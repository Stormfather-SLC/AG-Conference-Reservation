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
- **Change awareness on the Groups list** (built Oct 27). An Updated column, plus a dot on any group the organizer changed since you last opened it. The dot is remembered per browser, so each staff member sees what's new to them, and only organizer changes count. Opening the group (any action) or "Mark all as seen" clears it.
- **Guests with several restrictions** (built Oct 27). A compact one-line-per-guest list on the form; Add/Edit opens a dialog with a multi-select of restrictions and one "How serious" choice each (replacing separate Type and Severity). Duplicate names are offered a merge. Seriousness is optional so organizers aren't blocked by details they don't have; Celiac disease is its own choice and always treated as strict. Kitchen sheets count one special plate per guest (previously one per restriction, which over-counted). Per-guest meal attendance is still not asked: every listed guest is planned for every meal.
- **Meal and snack time changes** (built Oct 27 by Matt's decision). Organizers request a different time; Conference Services approves or declines from the Groups list (Review button opens a dialog) or changes a time directly on Rooms & locations. Every change is logged, and the production list opens with the day's time changes and any requests not yet approved.
- Hosting assumed at aspengrove.byu.edu.

### Still to confirm with Nate (breakout rooms and walk-throughs)

Built Oct 27 with these defaults; adjust after Nate reviews it.

1. **Setup styles** for breakout rooms: theater, round tables, classroom, boardroom, U-shape. Right list?
2. **Fees.** No fee note is shown for breakout rooms or walk-throughs. Should there be one, like mid-event room changes?
3. **Walk-through timing.** The form suggests before the 14-day lock-in deadline but allows any day before the event.
4. **Who updates rooms and walk-throughs.** Both save with the staff notes, which only artifact editors can change. Nate or his team need edit access, or these move to their own permission.
5. **When rooms get decided.** Room assignment on the page assumes Setup decides rooms ahead of the event week. If it's usually decided day-of, the printed write-in line remains the fallback.

## Phase 2

- **Staff edit a submission, with change history.** Partly built already: Conference Services can reopen a locked reservation and every save is logged.
- **Client edits or resubmits their own form.**
- **"Changed after lock-in" (quick follow-on).** Once locked in, organizers can't edit, so post-lock-in changes only happen when staff reopen a group, the same path as emailing a change today. When a reopened group is locked again, flag it "Changed after lock-in" on the Groups list, and mark on the Final sheet which sections changed since the first lock-in. Builds on the change history already recorded.
- **"Needs attention" report and daily digest for Lisa** (discussed Oct 27). One view of what the office has to act on: groups near or past the lock-in deadline, not started, changed since last viewed (especially headcount, allergies, and anything changed after lock-in), newly locked in, and upcharges by group. A once-a-day email digest, sent only when something is on that list, links to the report and carries no guest names or allergy details. For the pilot it could run as a scheduled task sending from Matt's Gmail; production would use BYU mail. **Quick follow-on.** To avoid spamming Lisa when a group changes something one day and changes it back the next, the digest compares each group with how it looked at the last digest, not with every edit, so changes that cancel out never appear. Drafts are only counted ("3 groups still working on their form"); changes after lock-in are listed individually. Open question: what Lisa's team spends the most time chasing, so that goes at the top.

## Parking lot

- Monday.com (forms and boards). Not part of the design.
- Pricing beyond what's on the PDF.
- Billing integration. At most a selections report to billing.
- Food order guide: plate counts across the week, with 15 staff meals added to the largest entrée at breakfast, lunch and dinner (not snacks). Moved out of Phase 1 on Oct 27 by Matt's decision. The staff meal count is already set in the app (`STAFF_MEALS`).
- Units or yields (pans, trays) on the production list and order guide.
- **Time-aware room bookings.** Give each room booking a start and end time and check conflicts by overlapping time, not just same day. This would allow splitting a group's main room within a day (e.g. Timp A in the morning, Fir in the afternoon) and stop flagging a room a group reuses at different times as double-booked. Parked Oct 27; build it if either case comes up in real bookings.
