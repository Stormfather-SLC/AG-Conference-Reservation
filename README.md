# AG Conference Reservation

A prototype web form that replaces the paper **Conference Final Details** form at BYU Aspen Grove. Group organizers fill in meals, snacks, room setup, A/V and guest allergies online, then lock in their final details. Conference Services tracks every group, prints final and kitchen sheets, and downloads backups.

**Status:** Pilot prototype. Paper forms are still accepted as a backup.

- **Live page:** https://claude.ai/artifact/9kSo7EiZ3AAYSrh96k4yud
- **Production plan:** https://claude.ai/code/artifact/15e2fdf0-af95-4361-8be4-0ee0bddf457b
- **Owner:** Matt Rowe, Catering Supervisor, Aspen Grove

## What it does

### Organizers
- Open a reservation from the invitation link (`…#AG-XXXXX`) or by entering its code. Aspen Grove starts every reservation (Conference Services › Start a group); organizers can't create one themselves.
- Group name and event dates are read-only for organizers once set, so they stay in step with the office's registration. A note says to call the office to change them. Conference Services can edit them; if a date change drops a day that has meals or snacks, staff confirm first, and that day's selections are kept aside (shown on the form with a Discard button) and come back if the dates include it again.
- Fill in six sections: group and contact, attendee notes, rooms and A/V (including breakout rooms and an optional walk-through request), allergies (with an optional guest-list upload), meals and snacks by day, and comments.
- Allergies show as a compact list, one line per guest with all their restrictions (and a search box once there are more than 15). Add a guest or Edit opens a dialog: the guest's name, a multi-select of allergens and diets plus anything not listed, and one "How serious" choice for each (intolerance; mild, severe or airborne allergy; medically prescribed). A name that's already listed offers to add to that guest instead. For large groups, the guest-list upload fills the list in one step.
- Menu rules are built in: each meal and snack is checked to include it (nothing is included by default), 3-item snack limit, vegetarian plates, fajita meat, breakfast extras ($1.50 per person for each, offering only what that breakfast doesn't already include), and an upgrade-cost estimate. Each day tab shows how many meals and snacks are included, and lock-in asks the organizer to confirm any day with none.
- Review everything on one page, then lock in. The confirmation says plainly that locking in means they're done editing and later changes need a call to the office. After lock-in a pop-up confirms they're all set and offers **Print or download final report**. The form becomes read-only.
- Anything still missing is listed above the Lock in button. Each item links straight to the field that needs it, missing fields are outlined in red, and a "Go to next" button in the side rail steps through what's left.
- Request a different time for any meal or snack with **Change time** in its header; the request covers the whole meal for every guest. The header and a notice under it show the request as pending until Aspen Grove approves or declines it, and the form then shows the outcome.
- Print the final report or save it as a PDF straight from the page (works in the GitHub Pages demo too); Download file also appears where downloads are available.
- Editing a time request that was already approved sends it back to pending for Aspen Grove to review again.

### Conference Services

Sections are grouped by who uses them: **Groups** (office and programs), **Kitchen**, and **Setup** (Rooms & A/V, Walk-throughs), with Backup & system check off to the side. The Conference Services button works as a home button: it always opens Groups (Current & upcoming). Within Kitchen and Setup, the browser remembers which page was last used.

- **Groups:** start a group from booking details and get a ready-to-send invitation email. See every group's status (Not started, In progress, Locked in, Past deadline) and progress. Copy a reminder that lists what's missing. Reopen or delete a reservation. An Updated column shows when each group last changed, and a dot marks groups the organizer changed since you last opened them (remembered per browser; opening the group or "Mark all as seen" clears it). The list shows current and upcoming groups; groups move to **Past groups** (read-only, searchable, Final sheet only) the morning after their last day.
- **Final sheet:** a printable one-page summary of each group.
- **Kitchen → Daily production list:** a printable daily list for the kitchen. Each meal and snack is split into servings: groups served at the same time and place are combined under one "Serve" count, and groups at a different time or place get their own block and count. Every entrée, side, included item and snack has a checkbox and a blank PAR line for the chefs. Each serving has a one-line special-plates summary; after the last service, special plates are listed once for the day by guest, followed by a short preview of tomorrow.
- **Kitchen → Weekly meal schedule:** an at-a-glance page for the week, then one page per day with every meal and snack in time order. Each service lists the groups first (guests, location, dietary count) with their meal or snack underneath; shared meals are marked, and only off-schedule times and places are highlighted. Each day ends with a dietary list, one line per guest. Dietary needs are listed once on the summary page; a guest attending only certain meals is also listed on each day they attend.
- **Setup → Rooms & A/V:** a printable weekly sheet for the setup crew. An at-a-glance table shows each day's groups, setup style, and A/V equipment out (with counts when groups overlap). Then one block per group: a blank line to write in the assigned room, breakout rooms (each with a blank room line and its A/V checklist), setup, changes during the event, setup notes, an "A/V Requirements" checklist of what the group requested, any meals or snacks served in the meeting room, and the on-site contact.
- **Rooms & locations** (one page per group, from Groups or Setup → Rooms & A/V): Setup assigns the main room for each day and a room for each breakout, with a warning when a room is already booked that day. Conference Services sets meal and snack locations below, including "Their meeting room", which follows the assigned room. Assigned rooms print on the Rooms & A/V sheet and Final sheet; unassigned ones print as a line to write in. Meal and snack times show here read-only, with changed ones marked. Staff change a time directly from Groups › Actions › Meal & snack times (for phone or email changes after lock-in); that dialog also holds the time change history. Organizers' time requests are reviewed from the Groups list: the amber "time change requests to review" link opens a dialog to approve or decline each one, and the production list opens with that day's time changes and any requests not yet approved.
- **Setup → Walk-throughs:** every walk-through request with the group's two preferred days, party size, and whether other groups in the system are on site those days. Mark each Scheduled (with the confirmed day and time), Done, or Couldn't schedule; the organizer sees the result on their form.
- **Backup & system check:** download the group list and meal list (CSV, opens in Excel) or a full backup (JSON). Run a save check.

## How saving works

The page runs as a Claude artifact. Data is stored in the artifact's shared database, not in this repository and not in the HTML file.

- Every change saves within about a second.
- If a save fails, a safety copy stays in that browser and the page retries on its own. If the person returns before it lands, the page offers to restore it.
- Each reservation keeps a change history: who changed which section, and when.
- Only artifact editors can change rooms, meal locations and walk-through status (database rule: `staffnotes` write = `admin`).

See [docs/data-model.md](docs/data-model.md) for the record format.

What's in this phase, what's next, and what's parked: [docs/roadmap.md](docs/roadmap.md).

## Running it

`index.html` is a single self-contained page with no build step.

- **Inside Claude (the live page):** shared saving, downloads and the change history all work.
- **Opened directly in a browser:** the page runs in demo mode and saves to that browser only. This is useful for reviewing screens and text, not for real use.
- **Published page, not signed in:** the page also runs in demo mode. Reservations made there are copied into the shared record the next time that person opens the page signed in on the same browser (the local copy is kept aside, not deleted).

## Demo (GitHub Pages)

The same `index.html` runs as a stand-alone demo on GitHub Pages (`*.github.io`) or at any address ending in `?demo`. The demo:

- never connects to the shared record and needs no sign-in;
- opens with six made-up sample groups whose dates move with today's date: two locked-in groups in camp the same week (Monday dinner–Friday breakfast and Tuesday lunch–Thursday dinner, the Monday of the week after next) so the kitchen list, weekly meal schedule and rooms show groups combined; one in progress and due soon; one with a pending time change; one invited but not started; and a past group;
- when a newer set of samples ships, it replaces the old samples on the next visit but keeps groups loaded from a file;
- has **Reset demo**, which puts the samples back, and **Load example file**, which loads a backup-format `.json` file (the same shape as Conference Services › Backup › Full backup).

Real examples (for example a group recreated from its paper packet) stay in a `.json` file on the presenter's computer and are loaded with **Load example file**. They are never committed: the repository and its Pages site are public, and `.gitignore` blocks `*.json`.

To turn the demo on: repository **Settings › Pages**, Source **Deploy from a branch**, branch `main`, folder `/ (root)`. The demo is then at `https://stormfather-slc.github.io/AG-Conference-Reservation/`.

## Known limits (pilot)

- Organizers must be signed in to Claude to save.
- Invitation and reminder emails are sent from the staff member's own email program: **Send email** opens a new message with the organizer's address, subject and text filled in, and the staff member presses Send there (the change history notes that it was opened to send). Nothing sends automatically. If the browser isn't set up to open the email program (common with Outlook on the web), use Copy message.
- In the demo, data lives in one browser, so an invitation link only opens the group on the computer that created it.
- There is no real staff sign-in. Guests see only the organizer view; the Conference Services tab appears in a simulated **staff view**, turned on with Alt+Shift+S, a link ending in `?staff` (demo: `?demo&staff`), or five quick taps on "Aspen Grove" in the header, and it lasts for that browser tab. This is for demos, not security: real sign-in comes with BYU hosting.
- The office phone number shown to organizers is `OFFICE_PHONE` near the top of the script (blank for now, so the text says "call the Aspen Grove office").
- Menus and prices are written into the code (`BREAKFAST`, `LUNCH`, `DINNER`, `SNACKS`, `VEG` near the top of the script).

The production plan covers what a live version needs: BYU sign-in, staff-managed menus, automatic reminders, and allergy-data retention rules.

## Data privacy

Never commit downloaded backups or exports. They contain guest names, phone numbers, emails and allergy information. `.gitignore` blocks `*.csv` and `*.json` files for this reason.
