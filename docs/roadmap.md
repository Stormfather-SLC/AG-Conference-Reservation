# Roadmap

How scope is decided: if the paper Final Details form does it, it's in scope. If the form doesn't do it, it waits for a later phase or the parking lot, and we say so before building it.

## Phase 1 (current)

Replace the PDF clients fill out with a web page that collects the same information, and build reports from what it collects.

- Web form covering everything on the PDF. Pricing is shown only as it appears on the PDF.
- Reports use only submitted data, as a snapshot. Changes after submission go through Conference Services by phone or email, as they do today.
  - Final sheet (one group)
  - Weekly meal schedule (kitchen; called "Weekly itinerary" until Oct 27)
  - Daily production list (kitchen)
  - Rooms & A/V (setup crew, weekly). Added Oct 23 by Matt's decision; room setup and A/V had been on the parking lot.
  - Walk-throughs (setup). See below.
- **Room assignment on the page** (added Oct 27 by Matt's decision). Setup assigns the main room per day and each breakout's room, with double-booking warnings; meals can be served in "their meeting room", which follows the assignment. Unassigned rooms still print as a write-in line.
- **Breakout rooms and walk-through requests.** Moved up from Phase 2 on Oct 27 by Matt's decision, at Nate's request (Programs manager, responsible for Setup). These go beyond the paper form.
  - The organizer says whether they need breakout rooms and, for each: purpose, people, days, times, setup style (theater, round tables, classroom, boardroom, U-shape), A/V and notes. Aspen Grove assigns the rooms, on the page or by writing them on the Rooms & A/V sheet.
  - The organizer can request a walk-through with two preferred days and times of day. The form says plainly that these depend on what else is happening at camp and aren't guaranteed. Setup staff mark each request Scheduled (with the confirmed day and time), Done, or Couldn't schedule; the organizer sees the result on their form.
- Hosting assumed at aspengrove.byu.edu.

### Still to confirm with Nate (breakout rooms and walk-throughs)

Built Oct 27 with these defaults; adjust after Nate reviews it.

1. **Setup styles** for breakout rooms: theater, round tables, classroom, boardroom, U-shape. Right list?
2. **Fees.** No fee note is shown for breakout rooms or walk-throughs. Should there be one, like mid-event room changes?
3. **Walk-through timing.** The form suggests before the 14-day lock-in deadline but allows any day before the event.
4. **Who updates rooms and walk-throughs.** Both save with the staff notes, which only artifact editors can change. Nate or his team need edit access, or these move to their own permission.
5. **Tree room order.** Combinations assume Spruce is between Fir and Pine. Confirm the middle room.
6. **When rooms get decided.** Room assignment on the page assumes Setup decides rooms ahead of the event week. If it's usually decided day-of, the printed write-in line remains the fallback.

## Phase 2

- **Staff edit a submission, with change history.** Partly built already: Conference Services can reopen a locked reservation and every save is logged.
- **Client edits or resubmits their own form.**

## Parking lot

- Monday.com (forms and boards). Not part of the design.
- Pricing beyond what's on the PDF.
- Billing integration. At most a selections report to billing.
- Food order guide: plate counts across the week, with 15 staff meals added to the largest entrée at breakfast, lunch and dinner (not snacks). Moved out of Phase 1 on Oct 27 by Matt's decision. The staff meal count is already set in the app (`STAFF_MEALS`).
- Units or yields (pans, trays) on the production list and order guide.
