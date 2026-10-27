# Data model

The page stores data in the artifact's shared database. There are three collections.

| Collection | Document id | Holds | Who can write |
|---|---|---|---|
| `reservations` | Reservation code, e.g. `AG-7KQ2M` | One group's final details | Any signed-in user of the page |
| `staffnotes` | Reservation code | Meal locations and time changes set by Conference Services, and walk-through status set by Setup | Artifact editors only |
| `health` | `check` | Timestamp from the last save check | Any signed-in user of the page |

## `reservations/{code}`

| Field | Type | Notes |
|---|---|---|
| `code` | string | `AG-` plus 5 characters (no 0, O, 1 or I) |
| `status` | `"draft"` or `"locked"` | Only an organizer locks; only Conference Services reopens |
| `createdBy` | `"staff"` or missing | `"staff"` when started from Conference Services |
| `group`, `contact`, `phone`, `email` | string | |
| `headcount` | number or `""` | Final headcount; the default guest count for every meal |
| `startDate`, `endDate` | `YYYY-MM-DD` | Up to 7 days |
| `onsite` | `{same, name, phone}` | On-site contact; `same: true` means the organizer |
| `attendeeNotes` | string | Partial attendance, arrivals and departures |
| `setup` | `"theater"`, `"rounds"` or `""` | Preferred setup for the main room |
| `roomChanges` | `"yes"`, `"no"` or `""` | Setup changes during the event |
| `setupNotes`, `avOther`, `comments` | string | |
| `noAV` | boolean | |
| `av` | string[] | From Projector, Screen, Whiteboard, Microphone, Speakers / sound, Easel & flip chart |
| `breakoutNeed` | `"yes"`, `"no"` or `""` | Whether the group needs breakout rooms |
| `breakouts` | Breakout[] | See below. Used only when `breakoutNeed` is `"yes"` |
| `walk` | Walk | Walk-through request; see below |
| `allergies` | Allergy[] | See below |
| `noAllergies` | boolean | Organizer confirmed there are none |
| `roster` | array or null | Imported guest list rows `{name, diet, allergy, type, severity}` |
| `rosterFile`, `rosterAt` | string | Name and upload time of the imported guest list |
| `days` | Day[] | One per event day; see below |
| `checklist` | `{schedule, payment}` | Booleans |
| `history` | Event[] | Change history, newest last, capped at 80 |
| `createdAt`, `updatedAt`, `lockedAt` | ISO timestamp | `lockedAt` is null until locked |

### Breakout

| Field | Values |
|---|---|
| `name` | Purpose or name, e.g. "Leadership session" |
| `people` | number or `""` |
| `days` | Event dates (`YYYY-MM-DD`) the room is used |
| `start`, `end` | `HH:MM` or `""` |
| `setup` | `"theater"`, `"rounds"`, `"classroom"`, `"boardroom"`, `"ushape"` or `""` |
| `av` | string[], same list as the main room |
| `notes` | Other A/V or setup notes |

To lock in, each breakout needs `people`, at least one day, and `setup`.

### Walk

`{want, choices: [{date, time}, {date, time}], people, notes}`

- `want`: `"yes"`, `"no"` or `""` (not answered; optional)
- `choices`: two preferred days; `time` is `"Morning"`, `"Afternoon"`, `"Any time"` or `""`. Not guaranteed.
- To lock in with `want: "yes"`, the first choice needs a date.

The staff side lives in `staffnotes/{code}.walk`: `{status, date, time, note}`, where `status` is `"requested"`, `"scheduled"`, `"done"` or `"cant"` (couldn't schedule). `date` and `time` are the confirmed walk-through.

### Allergy

| Field | Values |
|---|---|
| `name` | Guest name |
| `allergy` | One of the 9 major allergens, Vegan, Vegetarian, or free text when `other` is true |
| `other` | true when `allergy` is free text |
| `type` | `Allergy`, `Intolerance`, `Preference` or `Medical` |
| `severity` | `Mild`, `Severe` or `Airborne` (allergies only) |
| `mode` | `"all"` (every meal in the stay) or `"specific"` (only `meals`) |
| `meals` | Slot keys `YYYY-MM-DD|meal` when `mode` is `"specific"` |
| `from`, `to` | Slot keys limiting the stay window, or `""` |
| `src` | `"roster"` when imported from the guest list |

Severe means `type` is `Medical`, or the severity is `Severe` or `Airborne`.

### Day

`{date: "YYYY-MM-DD", meals: {breakfast, amSnack, lunch, pmSnack, dinner}}`

**Breakfast, lunch, dinner:**

| Field | Notes |
|---|---|
| `choice` | Menu item id, `"none"` (not needed), or `""` (not chosen yet) |
| `count` | Guests at this meal; `""` means use `headcount` |
| `meat` | `"Beef"` or `"Chicken"` (fajitas) |
| `addon` | Breakfast add-on, +$1.50 per person |
| `second` | Second protein, +$3 per person |
| `vegChoice`, `vegCount` | Vegetarian option id and number of plates |

**Snacks:** `{on, items (up to 3), count}`

Standard times: breakfast 8:00, morning snack 10:30, lunch 12:30, afternoon snack 3:00, dinner 6:00.

### Event (change history)

`{at, role, by, what, secs?}`

- `role`: `"organizer"` or `"staff"`
- `by`: the person's opaque user id. Names are looked up when shown, never stored.
- `what`: "Created by organizer", "Started by Conference Services", "Edited", "Locked in", "Reopened for changes", or "Restored unsaved changes from this device"
- `secs`: for "Edited", the sections changed. Edits by the same person within 30 minutes merge into one entry.

## `staffnotes/{code}`

`{code, locations, times, updatedAt}`

- `locations[slotKey]`: `{place, room, note}`. `place` is Dining hall, Conference room, Aspen Lobby, Boxed to go, or Other. Without an entry, meals default to the Dining hall and snacks to the Aspen Lobby.
- `times[slotKey]`: an `HH:MM` time when it differs from the standard. A changed time is flagged because a fee may apply.

A slot key is `YYYY-MM-DD|meal`, for example `2026-11-06|lunch`.

## Deadline

The lock-in deadline is 14 days before `startDate`.
