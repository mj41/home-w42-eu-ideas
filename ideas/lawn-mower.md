# A robotic lawn mower

**Status:** idea, 2026-10-02.

## Idea

The garden's robotic mower joins the home: its state (mowing, docked, stuck, rain
pause, battery), its position, and start / stop / dock commands, so loops can use it
("no mowing while the kids are in the garden", "mow when everyone is away") and
Stack-chan can tell you it is stuck.

## How it fits

An adapter ([architecture §4](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#4-adapters-and-data-sources)), and only for **high-level commands**: start, stop,
dock, schedule. Never remote driving of a machine with blades.

- **Open hardware:** the **OpenMower** project replaces the mainboard of some
  cheap mowers (the YardForce Classic 500 family) with open firmware, RTK GPS and
  ROS. A mower converted that way can be fully local.
- **Vendor mowers:** most talk only to their vendor cloud (Husqvarna Automower
  Connect, Worx Landroid, …). Some have local or semi-local interfaces that Home
  Assistant integrations use. Where only a cloud exists, the mower stays out, or
  joins through Home Assistant with that limit written down (principle: no vendor
  cloud in the data path).

## Safety

- Blades: no remote driving, no starting while a person is detected near it
  (presence from the Wi-Fi presence adapter and garden cameras is a loop's input,
  not a guarantee).
- The mower's own lift, tilt and bump sensors stay in charge.

## First step

List the mower actually in the garden, and check what local interface it has, if
any. If none, park this idea.

## Open questions

- Is RTK GPS position data treated like a person's location (it maps the garden
  and the house)?
