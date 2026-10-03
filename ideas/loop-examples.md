# Example loops

**Status:** ideas, 2026-10-02. Each is a candidate for the loop runtime
([architecture §7](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#7-the-controller-server-loops-and-ai)): written (often by an AI agent), replayed against recorded
events, run in shadow, then live after an owner's approval.

| Loop | Reads | Does | Notes |
|---|---|---|---|
| **Safety stop** | car sonar | turns forward drive into stop | exists, in [sbot](https://github.com/mj41/sbot) |
| Robot frowns while the car is blocked | sbot `safety_stop` decisions | Stackchan `emotion sad`, back to neutral when clear | first loop between two devices |
| Window shutters | HA temperatures, sun, weather, wind; presence | shutter positions over the day | a controller; replaces an HA automation ([window-shutters](window-shutters.md)) |
| Look at the door | door contact (Home Assistant) | Stackchan turns its head to the door, shows the door camera | |
| Vacuum when nobody is home | Wi-Fi presence, private GPS "away" | start the Roomba; dock when someone returns | replay on a week of presence first |
| Welcome home | Wi-Fi presence (a registered phone joined) | the pet greets that person by name | |
| School-day pet | calendar `school_day` | the pet's school routine follows the real calendar | |
| Kid's card | NFC SUN read on Stackchan | opens the kid's session with the kid's scopes | proxy permissions |
| No mowing with kids outside | garden camera `person_seen`, presence | pause the mower | safety-adjacent: the mower's own sensors stay in charge |
| Known car arrived | camera plate read (known plates only) | event + notification; opens the gate if granted | legal check first |
| Low battery | battery telemetry of any device | notify, or send a robot to its dock | |
| Line follower | car line sensors (raw) | drives the car along a line | a controller: runs with priority |

## Rules every loop follows

- Raw data in, decisions out, both in the event hub with causes.
- Only the scopes in its grant; read limits apply.
- A kill switch per loop, and "all loops off" for the home.
