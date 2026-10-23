# Roadmap

How scope is decided: if the paper Final Details form does it, it's in scope. If the form doesn't do it, it waits for a later phase or the parking lot, and we say so before building it.

## Phase 1 (current)

Replace the PDF clients fill out with a web page that collects the same information, and build reports from what it collects.

- Web form covering everything on the PDF. Pricing is shown only as it appears on the PDF.
- Reports use only submitted data, as a snapshot. Changes after submission go through Conference Services by phone or email, as they do today.
  - Final sheet (one group)
  - Weekly itinerary
  - Production list (kitchen, daily)
  - Rooms & A/V (setup crew, weekly). Added Oct 23 by Matt's decision; room setup and A/V had been on the parking lot.
  - Food order guide: plate counts across the week, with 15 staff meals added. **Not built yet.**
- Hosting assumed at aspengrove.byu.edu.

## Phase 2

- **Staff edit a submission, with change history.** Partly built already: Conference Services can reopen a locked reservation and every save is logged.
- **Client edits or resubmits their own form.**
- **Breakout rooms** (requested Oct 23). In the Conference room & A/V section, let the organizer request breakout rooms and say how each should be set up.
- **Pre-conference walk-through** (requested Oct 23). Let the organizer request a walk-through of the spaces the group will use.

### Open questions for breakout rooms and the walk-through

Settle these before building:

1. **Breakout room details.** What does the organizer give for each room: purpose or name, headcount, days and times, setup style, A/V? Is per-room A/V needed, or is the main room's A/V list enough?
2. **Setup styles.** The main room offers theater or round tables. Do breakouts need others, such as classroom, boardroom or U-shape?
3. **Room assignment.** The form doesn't record which room a group gets. Does Conference Services assign breakout rooms in the page (like meal locations), or write them in on the printed sheet?
4. **Walk-through: request or schedule.** A request (preferred dates and times, who's coming) that staff confirm by phone or email is a small change. Real scheduling against staff or room availability needs a calendar and is much larger.
5. **Walk-through timing.** Is there a cutoff, such as before the 14-day lock-in deadline? Is it in person only, or virtual too?
6. **Fees.** Do breakout rooms or mid-event breakout changes carry a fee to show on the form, like the main room's mid-event changes?

### What it touches

Organizer form section 03, the review page, the Final sheet, the Rooms & A/V sheet, the data model ([data-model.md](data-model.md)), and the group CSV export.

## Parking lot

- Monday.com (forms and boards). Not part of the design.
- Pricing beyond what's on the PDF.
- Billing integration. At most a selections report to billing.
- Units or yields (pans, trays) on the production list and order guide.
