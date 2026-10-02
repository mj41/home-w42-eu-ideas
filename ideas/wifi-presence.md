# Who is home: Wi-Fi client detection

**Status:** idea, 2026-10-02.

## Idea

The home router already knows which devices are on the Wi-Fi. Turned into events,
that is the simplest presence sensor: "a family member's phone joined", "the last
phone left". Loops build on it: start the vacuum when nobody is home, set the pet
to "waiting", lower the heating.

## How it fits

An adapter (architecture §4) that polls or subscribes to the router:

- **OpenWrt:** `ubus` (`hostapd.*` `get_clients` for associated stations, the DHCP
  leases), over `ubus` HTTP (rpcd) with a dedicated read-only user.
- **Other routers:** UniFi and MikroTik have APIs; consumer routers often only a
  web page. A fallback is the node itself watching ARP and DHCP on the LAN.
- **Raw events:** `client_joined {mac_id, band, rssi}`, `client_left {mac_id}`,
  plus periodic `rssi` per client. "Someone is home" is a loop, not the adapter.

## Privacy and security

- **Pseudonymize MACs** (a keyed hash per home). Only devices the owner registered
  ("Ema's phone") get names; guests and neighbours' devices stay anonymous ids, kept
  briefly.
- Phones use a random MAC per network; it is usually stable for one network, so
  presence still works, but the owner may need to re-register a phone after a reset.
- The router account is read-only.

## First step

An OpenWrt adapter (the home router, if it runs OpenWrt) that logs joins and leaves
of registered phones, and a "who is home" view in the cockpit.

## Open questions

- Phones sleep their Wi-Fi: how long a leave counts as "left" (a loop parameter,
  tested on recorded events with replay)?
- Combine with the private GPS app's "home / away" for a better answer?
