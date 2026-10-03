# Calendars and other personal data sources

**Status:** idea, 2026-10-02.

## Idea

The family's calendars feed the home's loops: school days, trips, guests, late
meetings. The pet already has school and night routines; with the calendar it knows
when school is actually on. The robot reminds a kid of the swimming lesson. The
heating knows the family is away until Sunday.

## How it fits

A personal-data adapter ([architecture §4](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#4-adapters-and-data-sources)):

- **Sources,** narrowest access first: a calendar's secret ICS address (one calendar,
  read-only), CalDAV (Nextcloud, Radicale, many providers), and only then Google or
  Microsoft APIs with a read-only scope for chosen calendars. API tokens are kept in
  the capture station on the person's laptop, never on the node (see
  [personal captures](personal-captures.md)).
- **Who pulls:** the node pulls ICS and CalDAV calendars (one calendar, read-only,
  no account access). API calendars are pulled by a collector in the capture station,
  which sends only the coarse events below. Nothing is pushed to the provider, and
  nothing writes to a calendar unless a permission says so.
- **Events in the hub are coarse:** `busy {person, from, to}`, `away {person,
  until}`, `school_day {kid}`. The titles and details stay with the calendar's
  owner and are readable only by them, or by a loop granted that calendar.

## Privacy and security

- Calendar access is a scope per person and per calendar.
- AI agents see coarse events, not titles, unless the person grants a task more.
- Reads are audited and shown to the calendar's owner ([architecture §8.4](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#84-auditing)).

Later sources with the same pattern: contacts (for recognising visitors), a shared
shopping list, school announcements.

## First step

One ICS link (a school or family calendar) → `school_day` events → the pet's school
routine follows the real calendar.

## Open questions

- Which provider does the family actually use, and does it offer CalDAV or only an
  API with OAuth?
