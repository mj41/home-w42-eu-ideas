# Personal captures: what I saved, from many apps

**Status:** idea, 2026-10-02.

## Who needs it and why

An adult who saves things "for later" in many apps and forgets them: [use case 13](https://github.com/mj41/home-w42-eu/blob/main/docs/use-cases.md#13-follow-up-on-what-i-saved),
"Follow up on what I saved" (home-w42-eu [use cases](https://github.com/mj41/home-w42-eu/blob/main/docs/use-cases.md)). The value is not
the data; it is the moment on Sunday evening when the home says "4 articles to read,
2 replies you promised, 1 task due Tuesday".

## Idea

Small collectors on the person's laptop pull **only the part of each account the
person chose** (one bookmarks folder, one group, one list) and send the extracted
items to the home node, where loops make digests and reminders.

## How it fits

home-w42-eu [architecture §4.1](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#41-personal-captures-from-third-party-accounts): a **capture station** (a separate OS user or a VM on
the laptop, one browser profile per service, an outbound allowlist), **tiny reviewed
collectors** (small Go programs, pinned by hash), and only `captured {source, kind,
title, url, saved_at, tags}` items going to the node (`class: collector`).

**Access per source**, narrowest first. A source that would need full account access
or scraping the logged-in website is not collected.

| Source | Narrowest access | Notes |
|---|---|---|
| Browser bookmarks: one folder (Chrome) or one tag (Firefox) | **read the local file**, no login: Chrome's `Bookmarks` JSON in the profile directory, Firefox's `places.sqlite` | the best case: no account, no token |
| Anything, from the phone | **"share to home"**: the phone's share sheet sends one link to the node (the old-phone / private light client) | works for every app, including those with no API |
| Saved posts on X | the API has a bookmarks read scope, but access tiers and terms change; otherwise share by hand | check the current terms before building |
| Saved posts on LinkedIn | no public API for saved items: share by hand, or the official data export | |
| A Messenger group | no API for personal chats (the Graph API is for business pages): the official "download your information" export of that one chat, or share by hand | never a logged-in browser session scraped by a program |
| Task lists | CalDAV tasks (VTODO), a plain file in a folder, or an API with a read-only scope (Google Tasks has `tasks.readonly`) | some task apps give only full-account tokens: then share by hand |
| Calendars | the calendar's secret ICS address (one calendar, read-only), or CalDAV | see [calendars](calendars.md) |

## Privacy and security

- **The account's credentials never leave the capture station**; the node and any AI
  agent only ever see extracted items.
- **No AI agent in the capture station.** Agents may read captures on the node, under
  the person's permission entries, with a local model by default.
- **Collectors are reviewed in full** (they are meant to be a few hundred lines), and
  any change is a new review and a new hash.
- **Captures belong to the person**: their store home, their read audit, short
  retention unless they keep an item.
- Exports and shares are what the person did themselves, so the risk of a stolen
  long-lived token does not exist for those paths.

## First step

The capture station with two collectors that need no account at all: one Chrome
bookmarks folder (local file) and "share to home" from the phone; the captures in the
person's store, and a weekly digest page.

## Open questions

- Capture station: a separate Linux user, a container, or a small VM? Which one is
  simplest to keep separate from the person's main browser profile?
- How to review collectors: a checklist plus an AI-assisted review, signed by the
  owner like a firmware manifest?
