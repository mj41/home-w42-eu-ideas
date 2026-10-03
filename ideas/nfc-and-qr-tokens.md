# NFC tags and QR codes as keys, triggers and labels

**Status:** partly working, 2026-10-02. Stackchan reads NFC tags (UID, type, NDEF
text), the pet uses NFC food cards, and browsers pair with devices by QR.

## Idea

Physical tokens are the friendliest interface a home has:

- **People:** a kid's NFC card held to the robot logs the kid in for that session,
  with the kid's scopes on that robot (a device as a proxy for a person's rights,
  [architecture §8.2](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#82-the-access-model-restricted-by-default)).
- **Guests:** the QR on a robot's screen gives a guest a small scope for an hour.
- **Things and places:** a tag on the door ("I'm leaving"), on the bedside table
  ("good night" routine), on toys and food cards for the pet.
- **Pairing:** QR codes pair browsers and new devices with the node (works today).
- **Switching what a device shows:** a scan starts a UI session (home-w42-eu
  [architecture §5.1](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#51-ui-sessions-a-scan-changes-the-devices-ui-then-it-comes-back)): Ema's card turns any robot into Ema's pet for a while, a QR on
  an appliance opens its page on your phone, and the device returns to its default UI
  when the session ends.

## How it fits

- A tag read is a **raw event** from the reader (`nfc_tag {uid, type, text}`); what
  it means is a loop's decision (principle: primary data only).
- **QR codes never name a host and keep their secret in the URL fragment**, so a
  relay never sees it ([architecture §10](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#10-connection-paths-local-first-w42eu-only-as-a-hub)).

## Security

- **A UID alone is not a key.** UIDs can be copied. Cards that carry a person's
  rights must prove themselves:
  - **NTAG 424 DNA** cards have SUN messages: every tap produces a new URL with a
    CMAC over a counter, verifiable by the node with the card's key. A copy replays
    an old counter and is refused.
  - Plain NTAG21x tags are fine for triggers and labels (a food card), not for
    rights.
- Cards are registered and signed by an owner; a lost card is revoked like a device.
- Rate limits on taps, so a reader cannot be used to brute-force anything.

## First step

Register a kid's NTAG 424 DNA card on the node; a tap on Stackchan opens the kid's
session in the pet app, with the kid's permissions only, and the robot returns to its
default face after 10 minutes without touch.

## Open questions

- Can Stackchan's ST25R3916 driver (our minimal port) read the SUN URL of an NTAG
  424 DNA, or does it need more of the ISO 14443-4 stack?
