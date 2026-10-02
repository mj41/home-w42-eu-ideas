# Local voice

**Status:** idea, 2026-10-02.

## Idea

Talk to the home through Stack-chan (and old phones) without a cloud. Stack-chan's
upstream AI.AGENT uses a third-party cloud (xiaozhi); this replaces it with speech
recognition and synthesis on the home node.

## How it fits

- Stack-chan already streams raw microphone PCM and plays PCM from the node
  (Embody Mode, LAN). The pet already speaks with Edge voice; this would make it
  local.
- On the node: speech to text (e.g. `whisper.cpp`), a local model for intent, text to
  speech (e.g. Piper). Results are events (`heard {text}`) that loops and apps use.
- A wake word on the device, or push-to-talk by head touch, so the microphone is not
  streamed all the time.

## Privacy

- The microphone streams only while listening, with the LIVE badge on.
- Transcripts follow the normal retention; audio is not stored.
- Hosted models only if the owner allows them for voice (architecture §8.5).

## First step

Push-to-talk on Stack-chan (hold the head), `whisper.cpp` on the node, the text as
an event in the cockpit's event list.

## Open questions

- Which node hardware runs speech to text fast enough in Czech and English?
