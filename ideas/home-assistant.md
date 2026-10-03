# Home Assistant's sensor array

**Status:** next, 2026-10-02 (roadmap stage 3). Home Assistant is the home's main
data source for now.

## Idea

Everything Home Assistant already reaches (Zigbee and Z-Wave sensors, smart plugs,
thermostats, door contacts, energy meters, weather, the many vendor integrations)
becomes data and commands for the home node, through one adapter.

## How it fits

An adapter ([architecture §4](https://github.com/mj41/home-w42-eu/blob/main/docs/architecture.md#4-adapters-and-data-sources)) using Home Assistant's **WebSocket API**:

- authenticate with a long-lived access token (kept on the node, never in a repo);
- `subscribe_events` for `state_changed`: each chosen entity becomes measurements
  (numbers) or events (on/off, open/closed) of a device in the node's registry;
- `call_service` for commands (switch a plug, set a temperature).

Home Assistant stays the hub for radios and vendor integrations it is good at, and
is **a data source, not the brain**. Over time, automations that need smarter
algorithms than HA supports move to controllers on the node (window shutters first,
see [window-shutters](window-shutters.md)). The node adds what HA lacks here:
owner-signed trust, per-device access control, read limits and audit, the event hub
with causes, and AI-written loops with replay.

## Privacy and security

- **Only chosen entities.** The adapter imports an allowlist, not "everything".
  Presence, cameras and location entities need their own scopes.
- The HA token can do anything in HA. Keep HA on the LAN, and the token only on
  the node.

## First step

A Go adapter that registers a handful of entities (a door contact, a temperature
sensor, a plug) as one device, so they appear in the event hub and can be used by a
loop: "when the door opens, Stackchan looks at the door".

## Open questions

- One node device per HA entity, per HA device, or per room?
- Over time, which integrations should move out of HA into native adapters?
