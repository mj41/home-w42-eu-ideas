# An old phone as a device

**Status:** idea, 2026-10-02.

## Idea

An old Android or Linux phone becomes a light client of the home node: camera,
microphone, speaker, screen, GPS, accelerometer, light sensor, battery and Wi-Fi,
all in one box that already exists in a drawer.

Uses: a camera at the door or the window, a wall screen for the cockpit, a baby
monitor, a second head for Stack-chan (a phone on the TPBot as the car's own
camera), a GPS tracker in the car.

## How it fits

A light client like Stack-chan (architecture §3): it registers `class: phone` with
the capabilities it really has, and streams media only while the node asks.

Three ways to build it, cheapest first:

1. **A web page (PWA) served by the node.** Camera and microphone through
   `getUserMedia`, motion and light through browser sensor APIs, GPS through
   geolocation. No install. Needs HTTPS on the LAN (browsers give camera and GPS
   only to secure pages), which the node needs anyway (its own certificate, or the
   self-signed one stackchan-server already makes).
2. **Termux plus a Go binary** on old Android: the same light-client code as the
   adapters, with `termux-api` for camera, sensors, GPS and notifications. Runs in
   the background better than a browser tab.
3. **A small native app** (Go core through `gomobile`, a thin Android UI) when the
   first two hit limits: background camera, boot start, locked screen.

On Linux phones (postmarketOS, Mobian) the Go light client runs directly.

## Privacy and security

- The phone shows what it streams (a LIVE indicator, like Stack-chan's).
- Camera and location are separate scopes, never implied.
- A phone left at home as a camera is a device of the home, not a person's proxy;
  a person's own phone is their proxy (architecture §8.2).

## First step

The PWA: a page at `https://<node>/device` that registers the browser as a device
with camera, GPS and screen, and shows up in the sbot cockpit next to Stack-chan.

## Open questions

- How old can the Android be? Browsers on Android 7 and older lack parts of the
  sensor APIs.
- Battery: keep the phone on a charger with a timer plug, or watch its battery
  health (old batteries swell).
