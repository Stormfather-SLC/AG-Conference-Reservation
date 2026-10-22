# AG Conference Reservation

A prototype web form that replaces the paper **Conference Final Details** form at BYU Aspen Grove. Group organizers fill in meals, snacks, room setup, A/V and guest allergies online, then lock in their final details. Conference Services tracks every group, prints final and kitchen sheets, and downloads backups.

**Status:** Pilot prototype. Paper forms are still accepted as a backup.

- **Live page:** https://claude.ai/artifact/9kSo7EiZ3AAYSrh96k4yud
- **Production plan:** https://claude.ai/code/artifact/15e2fdf0-af95-4361-8be4-0ee0bddf457b
- **Owner:** Matt Rowe, Catering Supervisor, Aspen Grove

## What it does

### Organizers
- Create a reservation, or open one from an invitation link (`…#AG-XXXXX`).
- Fill in six sections: group and contact, attendee notes, room and A/V, allergies (with an optional guest-list upload), meals and snacks by day, and comments.
- Menu rules are built in: 3-item snack limit, vegetarian plates, fajita meat, add-ons, and an upgrade-cost estimate.
- Review everything on one page, then lock in. The form becomes read-only.
- Download a printable copy.

### Conference Services
- **Groups:** start a group from booking details and get a ready-to-send invitation email. See every group's status (Not started, In progress, Locked in, Past deadline) and progress. Copy a reminder that lists what's missing. Reopen or delete a reservation.
- **Final sheet:** a printable one-page summary of each group.
- **Meal locations:** set where and when each meal is served.
- **Kitchen by day:** every group on site for a date, meal by meal, with plate, vegetarian and allergy totals.
- **Weekly itinerary:** every meal and snack break for a week, days across and meals down, for every group on site. Shows guests, menu, vegetarian plates, allergy counts, and any time or location that differs from the standard. Prints landscape.
- **Backup & system check:** download the group list and meal list (CSV, opens in Excel) or a full backup (JSON). Run a save check.

## How saving works

The page runs as a Claude artifact. Data is stored in the artifact's shared database, not in this repository and not in the HTML file.

- Every change saves within about a second.
- If a save fails, a safety copy stays in that browser and the page retries on its own. If the person returns before it lands, the page offers to restore it.
- Each reservation keeps a change history: who changed which section, and when.
- Only artifact editors can change meal locations (database rule: `staffnotes` write = `admin`).

See [docs/data-model.md](docs/data-model.md) for the record format.

## Running it

`index.html` is a single self-contained page with no build step.

- **Inside Claude (the live page):** shared saving, downloads and the change history all work.
- **Opened directly in a browser:** the page runs in demo mode and saves to that browser only. This is useful for reviewing screens and text, not for real use.

## Known limits (pilot)

- Organizers must be signed in to Claude to save.
- Invitation and reminder emails are copied and pasted. Nothing sends automatically.
- The Conference Services tab is not behind a separate staff sign-in.
- Menus and prices are written into the code (`BREAKFAST`, `LUNCH`, `DINNER`, `SNACKS`, `VEG` near the top of the script).

The production plan covers what a live version needs: BYU sign-in, staff-managed menus, automatic reminders, and allergy-data retention rules.

## Data privacy

Never commit downloaded backups or exports. They contain guest names, phone numbers, emails and allergy information. `.gitignore` blocks `*.csv` and `*.json` files for this reason.
