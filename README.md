# home-w42-eu-ideas

Ideas for devices, adapters, apps and loops for
**[home-w42-eu](https://github.com/mj41/home-w42-eu)**, a local first, privacy first
platform for a home (its vision, use cases, principles and architecture live there; so
does the list of [its repos](https://github.com/mj41/home-w42-eu#the-repos-today)).
One file per idea. **Every idea starts from the people it is for**: which use case it
serves (home-w42-eu [use cases](https://github.com/mj41/home-w42-eu/blob/main/docs/use-cases.md)), or which new use case it adds. An idea
moves into the architecture only when it changes the design.

> **Ideas, written with AI agents**, not reviewed by others yet, and not promises.
>
> **Want one of them built?** Ask in the [issues](https://github.com/mj41/home-w42-eu-ideas/issues), and ideally [sponsor mj41](https://github.com/sponsors/mj41) on
> GitHub: mj41 codes for attention food.

| Idea | Kind | Status |
|---|---|---|
| [Stackchan on wheels (TPBot)](ideas/stackchan-on-wheels.md) | device + adapter + app | **POC works** |
| [NFC tags and QR codes](ideas/nfc-and-qr-tokens.md) | interface, access | **partly works** (NFC reads, QR pairing) |
| [An old phone as a device](ideas/old-phone-as-device.md) | light client | idea |
| [Stackchan on an old Roomba](ideas/roomba.md) | adapter, mobile base | idea |
| [A robotic lawn mower](ideas/lawn-mower.md) | adapter | idea |
| [Home Assistant's sensor array](ideas/home-assistant.md) | adapter | next (roadmap stage 3) |
| [Window shutters controller](ideas/window-shutters.md) | device + controller | hardware and software exist; roadmap stage 4 |
| [A private, audited location app](ideas/private-gps-app.md) | light client, privacy | idea |
| [Cameras and plate recognition, locally](ideas/cameras-and-plate-ocr.md) | adapter, vision | idea |
| [Who is home: Wi-Fi presence](ideas/wifi-presence.md) | adapter | idea |
| [Calendars and personal data sources](ideas/calendars.md) | adapter, personal data | idea |
| [Personal captures: what I saved, from many apps](ideas/personal-captures.md) | collectors, personal data | idea |
| [Local voice](ideas/local-voice.md) | interface | idea |
| [Repurposing old hardware](ideas/repurpose-old-hardware.md) | overview | idea |
| [Example loops](ideas/loop-examples.md) | loops | two run: the safety stop (controller) and `frown` (loop) |

## Adding an idea

Copy this outline into `ideas/<short-name>.md`:

```markdown
# Title

**Status:** idea | exploring | POC works | done, <date>.

## Who needs it and why
The person, the moment in their day, and the use case it serves
(home-w42-eu [use cases](https://github.com/mj41/home-w42-eu/blob/main/docs/use-cases.md)). Start here, not from a device or a protocol.

## Idea
What it is.

## How it fits
Light client, adapter, app or loop ([architecture §3–§7](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#3-light-clients)); its capabilities; prior art.

## Privacy and security
Which scopes, what is kept and for how long, what could go wrong.

## First step
The smallest thing that proves it on real hardware.

## Open questions
```

Every idea follows the principles (home-w42-eu [principles](https://github.com/mj41/home-w42-eu/blob/main/docs/principles.md)): raw data from
devices, restricted by default, short retention, no vendor cloud in the data path.

## License

Apache License 2.0, see [LICENSE](LICENSE).
