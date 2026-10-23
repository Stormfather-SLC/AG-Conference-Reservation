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
- Anything still missing is listed above the Lock in button. Each item links straight to the field that needs it, missing fields are outlined in red, and a "Go to next" button in the side rail steps through what's left.
- Download a printable copy.

### Conference Services
- **Groups:** start a group from booking details and get a ready-to-send invitation email. See every group's status (Not started, In progress, Locked in, Past deadline) and progress. Copy a reminder that lists what's missing. Reopen or delete a reservation.
- **Final sheet:** a printable one-page summary of each group.
- **Meal locations:** set where and when each meal is served.
- **Production list:** a printable daily list for the kitchen. Each meal and snack is split into servings: groups served at the same time and place are combined under one "Serve" count, and groups at a different time or place get their own block and count. Every entrée, side, included item and snack has a checkbox and a blank PAR line for the chefs. Each serving has a one-line special-plates summary; after the last service, special plates are listed once for the day by guest, followed by a short preview of tomorrow.
- **Weekly itinerary:** an at-a-glance page for the week, then one page per day with every meal and snack in time order. Each service lists the groups first (guests, location, dietary count) with their meal or snack underneath; shared meals are marked, and only off-schedule times and places are highlighted. Each day ends with a dietary list, one line per guest. Dietary needs are listed once on the summary page; a guest attending only certain meals is also listed on each day they attend.
- **Rooms & A/V:** a printable weekly sheet for the setup crew. An at-a-glance table shows each day's groups, setup style, and A/V equipment out (with counts when groups overlap). Then one block per group: a blank line to write in the assigned room, setup, changes during the event, setup notes, an "A/V Requirements" checklist of what the group requested, any meals or snacks served in the meeting room, and the on-site contact.
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
