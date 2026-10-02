# Stack-chan on an old Roomba

**Status:** idea, 2026-10-02.

## Idea

An old iRobot Roomba becomes a mobile base: a vacuum when that is its job, and a
platform that carries Stack-chan (or an old phone) around the home as a moving
camera and face. The TPBot car proved the pattern on a small scale.

## How it fits

An adapter (architecture §4) that offers the same kind of capabilities as the car:
`drive` (velocity and radius), `stop`, `clean`, `dock`, and raw telemetry (bumpers,
cliff sensors, wheel drops, encoders, battery, charging state).

- **Older models (500, 600, 700, 800 series)** have the **iRobot Open Interface**:
  a 7-pin mini-DIN serial port, TTL level, 115200 baud on most of them (57600 on
  some older ones). Commands such as Start, Safe, Full, Drive and Stream are
  documented in the public OI specification.
  - Adapter: an ESP32 (or a micro:bit) on the port, BLE or Wi-Fi to the node or to
    Stack-chan. The port supplies battery voltage (about 14 V), so the adapter needs
    a step-down regulator.
- **Newer Wi-Fi models (900, i, j, s series)** have no serial port, but many expose
  a local MQTT interface (used by open-source projects such as `dorita980` and Home
  Assistant's Roomba integration) once the local password is read from the robot.
  That is an adapter that needs no hardware, but it is clean / dock / status only,
  not free driving.

## Safety

- The OI "Safe" mode keeps the cliff and wheel-drop sensors active; never use
  "Full" mode for remote driving.
- Same layers as the car: a watchdog in the adapter (stop without a fresh drive
  command), and the node's safety controllers using the Roomba's own bumpers and
  cliff sensors.
- A Stack-chan riding on top needs a mount and a check of the weight and the
  centre of gravity.

## First step

Find which Roomba is available, check for the OI port, and drive it from the
laptop with a USB-serial cable and a small Go program before building the ESP32
adapter.

## Open questions

- Does a Roomba with Stack-chan on top still pass under furniture, and does the
  camera see anything useful from that height?
- Vacuuming and carrying the robot at the same time, or one job at a time?
