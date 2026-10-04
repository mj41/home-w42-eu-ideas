# Stackchan on wheels (TPBot)

**Status:** POC works, 2026-10-01/02. Repos: [tpbot-ble](https://github.com/mj41/tpbot-ble),
[StackChan fork](https://github.com/mj41/StackChan/tree/embody-mj41) (`car_ble`),
[s-w42-eu-sbot](https://github.com/mj41/s-w42-eu-sbot).

## What works

- micro:bit V2 in a TPBot V1, TinyGo firmware: BLE, raw sonar, line sensors and
  buttons, motors, headlights, a 500 ms watchdog.
- Driven first through the laptop (`tpbot-bridge`), then through Stackchan's own
  BLE, with the same `car_*` capability.
- sbot cockpit: video, joystick, drive pad, head pad, robot and car lights; the
  sonar safety stop (tested at 5–9 cm while driving).
- Stackchan riding on the TPBot, driven by looking through its camera.

## What is next

- **Latency through Stackchan** (~0.8 s per command): run car commands straight
  from the client callback instead of the app loop.
- **Stability:** the link dropped once when the micro:bit went silent, probably
  power. Report the micro:bit's supply voltage as telemetry.
- **BLE security:** anyone nearby can connect to the car. Allowlist Stackchan's
  address, or pair.
- **Loops:** the robot reacts to the car (frowns while blocked), line following as a
  loop from raw line-sensor data, "return to start".
- **A better camera position** on the car for driving.
