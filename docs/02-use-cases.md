# 02 — Use Cases

A unified SSID is not just a neat trick. It solves concrete problems. This
chapter walks through where it pays off, starting with the Philippine home
context most readers will recognize.

## Home and home-lab

The typical Philippine fiber setup looks like this:

- The ISP installs an **ONT** (optical network terminal) or a combined ONT/router
  near the entry point of the fiber.
- The stock router broadcasts wi-fi, often with a single SSID already, or with
  separate `_5G` networks depending on firmware and model.
- The router usually sits in the living room or beside the TV, while bedrooms,
  the home office, and the second floor are far away.

Problems this creates:

- **Dead spots** far from the router.
- **Hitting an invisible wall:** you move to the bedroom and the phone stays
  connected to the far 2.4 GHz radio with one bar instead of switching to a
  nearer AP (the "sticky client" problem — see [04-roaming.md](04-roaming.md)).
- **Two networks to manage:** family members connect to either `HomeWiFi` or
  `HomeWiFi_5G` and wonder why speeds differ.

A unified SSID with a second AP (or mesh node) fixes the day-to-day experience:
one network, best available radio, transparent movement.

**Concrete wins**

- Walking around during a video call or Messenger call without it dropping.
- Consistent name and password for guests — no "which one is 5G?" questions.
- New devices connect once and stay connected everywhere in the house.
- 2.4 GHz is left free for the devices that genuinely need it (see below).

## Small office and home office

- Staff and guests join the same main network regardless of proximity to which
  AP.
- VoIP and video meetings benefit from faster roaming between APs.
- A separate unified **guest SSID** (also spanning all APs) keeps visitors off
  the internal network.

The "unified" principle applies to the guest network too: if the guest SSID only
exists on one AP, guests lose signal when they move.

## Hospitality: hotels, cafes, Airbnbs

- Guests expect one network name they can join quickly.
- Multiple APs must share the SSID so coverage is seamless across floors and
  rooms.
- Band steering helps denser environments, where 2.4 GHz is congested by
  neighbors and by guest devices.
- Combined with a captive portal or voucher system, the SSID stays constant while
  authentication differs — an important separation of concerns (see
  [06-security.md](06-security.md)).

## IoT and smart-home devices

Many IoT devices — smart plugs, cameras, older printers, robot vacuums — only
support **2.4 GHz** and sometimes only older security modes.

Two common approaches:

1. **One unified SSID** where 2.4 GHz is available for these devices, and band
   steering keeps capable phones/laptops on 5 GHz. This works when the IoT gear
   can handle your security settings.
2. **A dedicated `IoT` SSID** on 2.4 GHz only, often on a separate VLAN. Best for
   security and for devices that refuse WPA3 or that steer poorly.

Both are valid. Use a unified main SSID plus a separate IoT SSID when you have
many cheap devices and want to isolate them.

## Campus / multi-AP / large spaces

- Dozens to hundreds of APs share the same SSIDs across the whole site.
- 802.11k/v/r become essential at this scale, as does proper transmit-power
  tuning to encourage roaming and reduce interference.
- This is where a **controller** (or controllerless cloud management) earns its
  keep — see [05-architecture.md](05-architecture.md).

## When *not* to unify

Unifying is a good default, but there are reasons to keep networks separate:

- **Legacy device that only speaks WPA2** while you want WPA3-only on the main
  network.
- **Device that ignores band steering** and you need it pinned to a band for
  reliability (some cameras, some doorbells).
- **Security isolation** — always separate guest and IoT traffic from trusted
  devices.
- **Troubleshooting** — temporarily splitting bands makes it easy to prove which
  radio a device is using.

None of these argue against unified SSIDs generally; they argue for *additional,
purpose-built* SSIDs alongside the unified one.

## Summary table

| Environment        | Unified SSID? | Notes                                               |
| ------------------ | ------------- | --------------------------------------------------- |
| Home / home-lab    | Yes           | Add AP/mesh for coverage; enable band steering      |
| Small office       | Yes + guest   | Keep guest unified across all APs                   |
| Hotel / cafe       | Yes + guest   | Captive portal handles auth, SSID stays constant    |
| IoT-heavy home     | Yes + IoT SSID| IoT on 2.4 GHz, isolated on its own SSID/VLAN       |
| Campus             | Yes (many APs)| Controller + k/v/r + power tuning required          |
| Legacy-only device | Main + extra  | Keep a compatibility SSID if needed                 |

## Next

- Band steering in depth: [03-band-steering.md](03-band-steering.md)
- <a id="use-cases-verify"></a>Checklist:
  - Identify the two biggest dead spots in your home.
  - List any devices that are 2.4 GHz-only (IoT, older gear).
  - Decide whether a guest SSID is needed.
