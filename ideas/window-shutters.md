# Window shutters controller

**Status:** hardware and software exist (custom, mj), 2026-10-02. Roadmap stage 4.

## Idea

The home's custom window shutters join the platform as a device, and their control
algorithm runs as a **controller on the node**. They are the first automation taken
away from Home Assistant, because good shutter control needs more than HA's
automations can express.

## How it fits

- **Device:** the existing shutter hardware and software, connected as a light client
  or through an adapter (wire protocol), with raw state (position per shutter, motor
  running, end stops) and commands (move to a position, stop).
- **Inputs:** Home Assistant as the data source (temperatures inside and out, sun,
  weather, wind), plus presence and calendars when those adapters exist.
- **Controller:** consumes those events from the hub, decides positions over the day
  (sun position and heat, glare, privacy at night, wind protection, nobody home), and
  logs every decision with its cause. It goes replay → shadow → live like every loop.
- **Safety and overrides:** wind or ice protection wins over comfort; a person pressing
  a physical switch wins over the controller, for a while.

## First step

Document the existing hardware and software's interface (what it reports, what it
accepts), then connect one shutter as a device and run today's logic in shadow mode
next to it, comparing decisions.

## Open questions

- Does the existing software stay the low-level driver (limits, motor timing), with the
  node only sending target positions? That keeps safety close to the hardware.
- Which inputs does the current algorithm already use, and which are missing?
