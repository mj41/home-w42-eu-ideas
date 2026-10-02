# A private, audited location app

**Status:** idea, 2026-10-02.

## Idea

A small open-source Android app that sends your location **only to your own home
node**, encrypted end to end, and shows you exactly what it sent, when, and who on
the node read it. The family can see where everyone is, without a company in
between.

## How it fits

The phone is a person's proxy device (architecture §8.2), registered as a light
client with one capability: location (and battery, so "low battery" is a loop's
input, not a mystery).

- **Prior art first:** **OwnTracks** (open source, on F-Droid) already sends
  location to your own server over HTTP or MQTT, with end-to-end encryption. An
  OwnTracks adapter on the node is the cheap first step.
- **Our own app**, if OwnTracks does not fit: Go core through `gomobile`, a thin UI,
  no Google Play services (plain `LocationManager`), on F-Droid with reproducible
  builds.

## Privacy and audit

- **To the node only,** pinned to the node's certificate, through the blind relay
  when away. No third party sees a location.
- **Precision is the person's choice:** exact, coarse (about 1 km), or only
  "home / away" decided on the phone. For location, the person's choice beats the
  raw-data rule.
- **History off by default.** With history on, the normal 7-day retention applies.
- **The app's audit page:** every fix sent (time, precision), and every read of it
  on the node (who, which app or loop, how much), from the node's read audit
  (architecture §8.4).
- **Read limits:** a loop may ask "is she home?", not download a week of tracks
  (architecture §8.3).
- A visible notification while it reports, as Android requires anyway.

## First step

An OwnTracks adapter on the node: one family member's phone, coarse precision,
"home / away" events in the event hub, and the read audit page.

## Open questions

- Kids' phones: who controls the precision, the kid or the parent, and when does
  that change (control could move to the kid as they grow up)?
- Battery cost of frequent fixes on old phones.
