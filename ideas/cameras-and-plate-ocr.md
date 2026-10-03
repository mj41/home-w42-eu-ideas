# Cameras and number-plate recognition, locally

**Status:** idea, 2026-10-02.

## Idea

IP cameras (and old phones, and Stack-chan) feed the home node, which detects
people, animals and cars and reads number plates, **on the node**, with no cloud.
Loops then do useful things: "the car of a family member arrived: open the gate",
"an unknown car parked for an hour: tell me", "a parcel was left at the door".

## How it fits

- **Cameras** join through an RTSP adapter ([architecture §4](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#4-adapters-and-data-sources)). Cloud features of the
  cameras are switched off, and the cameras are kept on a network that cannot reach
  the internet.
- **Detection and OCR** run on a home node with enough compute (an old laptop with a
  GPU, or a board with an NPU or a Coral accelerator).
- **Prior art:** **Frigate** (local NVR with object detection), and open-source
  plate readers (for example the ONNX-based `fast-alpr` / `fast-plate-ocr`, and the
  older OpenALPR). Frigate could be an adapter itself, as with Home Assistant.
- Results are events: `person_seen {camera}`, `car_seen {camera}`,
  `plate_read {camera, plate | hash}`.

## Privacy, law and security

- **Point cameras at your own property.** In the EU (GDPR) a private camera that
  covers a public street or a neighbour's property is a legal problem; plates are
  personal data. Check the local rules (in Czechia: the Office for Personal Data
  Protection) before covering any public area.
- **Known plates only.** The owner keeps a list (family, regular visitors). Only
  those are named in events; every other plate is kept as a salted hash for a short
  time, so "the same unknown car came back" works without a readable record.
- **No footage by default.** Frames are streamed while watched; clips are stored
  only when a loop asks, with a short retention per camera.
- Media scopes are never implied; reads are audited.

## First step

One camera at the house's own entrance, an RTSP adapter, person and car detection
on the node, events in the log. Plates later, after the legal check.

## Open questions

- Which node hardware gives enough frames per second at acceptable power?
- Frigate as an adapter, or our own detection pipeline in Go (calling an ONNX
  runtime)?
