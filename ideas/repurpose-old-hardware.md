# Repurposing old hardware

**Status:** idea, 2026-10-02.

## Idea

Before anything is thrown away, check if it can become part of the home:

| Old thing | New job |
|---|---|
| Laptop | **home node** (its battery is a built-in UPS), or the GPU node for vision and local AI |
| Tablet | wall screen for the cockpit and "who is home" (the PWA) |
| Phone | camera, GPS tracker, baby monitor, Stack-chan's second screen ([old phone](old-phone-as-device.md)) |
| USB webcam | camera on the node itself (V4L2), no network needed |
| Wi-Fi smart plugs and bulbs | reflash with **Tasmota** or **ESPHome** where the chip allows it, so they talk only to the home (local MQTT or the ESPHome API) |
| ESP32 / ESP8266 boards, micro:bits | sensors and adapters (as the micro:bit in the TPBot) |
| Robot vacuum | a mobile base ([Roomba](roomba.md)) |
| Old router | OpenWrt, then a presence sensor ([Wi-Fi presence](wifi-presence.md)) or a separate network for cameras |

## How it fits

Each one is a light client or an adapter ([architecture §3, §4](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#3-light-clients)). "Simple switches"
([principle 18](https://github.com/mj41/home-w42-eu/blob/main/docs/principles.md)): the same old tablet can be the cockpit in the morning and the
pet's big screen in the afternoon.

## Security

- Old Android and old router firmware have known holes: keep them on a separate
  network that reaches only the node, never the internet.
- Reflashed devices get device keys like everything else, once the trust stages
  are done.

## First step

An inventory: what old hardware is at home, and which row above it fits.
