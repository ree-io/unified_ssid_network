# 03 — Band Steering

Band steering is the technique most closely tied to unified SSIDs. This chapter
explains the bands, what steering does, how it works, and when it backfires.

## The bands at a glance

| Band     | Typical speed       | Range / wall penetration | Congestion      | Best for                          |
| -------- | ------------------- | ------------------------ | --------------- | --------------------------------- |
| 2.4 GHz  | Slower              | Best (goes far, through walls) | High (many neighbors, IoT) | Long range, IoT, legacy devices |
| 5 GHz    | Fast                | Moderate                 | Moderate        | Phones, laptops, streaming        |
| 6 GHz    | Fastest (Wi-Fi 6E/7)| Shortest                | Low (so far)    | Modern devices, dense areas       |

Higher frequency means more data capacity but shorter range and worse wall
penetration. That tradeoff is the whole reason band steering exists.

## The problem steering solves

If you simply give both bands the same SSID and do nothing else, many clients
will:

- connect to the **first** network they find at boot, often 2.4 GHz, and
- **stay** there even when a much faster 5 GHz radio is available.

Result: a modern phone sits on a slow, congested 2.4 GHz link while the 5 GHz
radio is nearly idle. Band steering exists to move capable clients onto the
better band.

## What "steering" actually means

There are two fundamentally different approaches, and it matters which one your
hardware uses:

### 1. Steering (nudging)

The AP encourages a dual-band client to choose 5 GHz but does not forbid 2.4 GHz.

Common mechanisms:

- **Probe suppression / delayed response:** the AP withholds or delays its 2.4 GHz
  probe responses to a client that is also probing 5 GHz, nudging the client to
  associate on 5 GHz first.
- **802.11k/v assist:** the AP tells the client about better candidates
  (neighbors) and can suggest a transition. See [04-roaming.md](04-roaming.md).
- **Band preference hints:** some standards-assisted methods (e.g. related to
  802.11ax/be signaling) advertise band preference.

Steering is *best-effort*. A client is free to ignore it. Most modern phones and
laptops cooperate; cheap IoT gear often does not.

### 2. Forcing

Some systems (often called "band lock" or per-device band control, more common in
mesh apps and enterprise gear) enforce a band. This is not steering — it is a
hard rule. It is powerful but can break devices that misbehave when locked.

Know which one you have. A toggle labeled "Band Steering" or "Smart Connect"
usually means option 1. Per-device options like "lock to 5 GHz" mean option 2.

## Single SSID vs split SSID, revisited

Band steering only makes sense when the SSID is **unified**. If the bands have
different names, the client cannot be steered between them at all — it would have
to disconnect and rejoin a different network.

However, keeping bands **split** is a legitimate troubleshooting and
compatibility tool:

- Split temporarily to confirm which band a stubborn device is on.
- Keep a device on a dedicated 2.4-only SSID when it steers badly.
- Keep WPA2-only devices on their own SSID if the main network uses WPA3-only.

The pragmatic configuration for most homes:

- **Main SSID:** unified across 2.4 + 5 (+ 6) GHz, band steering **on**.
- **Optional IoT SSID:** 2.4 GHz only, for devices that need it.
- **Optional guest SSID:** unified across all APs, isolated from the LAN.

## How to tell if band steering is working

You generally cannot see steering from the router UI directly. Practical tests:

1. Stand close to the AP with a dual-band phone; confirm it is on 5 GHz (look at
   the link details in the phone's Wi-Fi info, or use a Wi-Fi analyzer app).
2. Reboot the phone's wi-fi, or toggle wi-fi off/on, and watch which band it
   picks.
3. Walk to the far edge of coverage. Does the phone fall back to 2.4 GHz
   gracefully, or drop entirely?
4. Compare throughput on each band with a speed test at the same location to
   confirm the phone actually moved.

If a modern phone stubbornly stays on 2.4 GHz near the AP, steering may be off,
the firmware may implement it weakly, or the client may be ignoring it.

## Tradeoffs and pitfalls

- **Over-aggressive steering** can cause repeated failed associations, especially
  with older clients, leading to "cannot connect" complaints. If devices fail to
  join, weaken or disable steering and test again.
- **Weak signal on 5 GHz:** steering a client to 5 GHz when it is far away gives
  it a *worse* experience. Good implementations only steer when 5 GHz signal is
  adequate.
- **IoT fallout:** some smart devices refuse to join at all when steering is
  aggressive. Their usual fix is the dedicated 2.4 GHz IoT SSID.
- **No open standard for perfect steering:** it is vendor-behavior territory. The
  same client can steer well on one router and badly on another.
- **6 GHz adds a third choice:** Wi-Fi 6E/7 systems steer among three bands, and
  6 GHz is often "preferred" for capable clients, with 5 GHz as the next step and
  2.4 GHz as the fallback.

## Interaction with roaming

Band steering moves a client *between bands on the same or nearby AP*. Roaming
moves a client *between APs*. A device may do both as you walk around. They are
separate mechanisms but often implemented together under one "smart" feature.
Details are in [04-roaming.md](04-roaming.md).

## Recommended starting settings (generic)

- Unified SSID across all bands.
- Security: WPA2/WPA3 mixed mode (transition mode) unless all your devices
  support WPA3 (see [06-security.md](06-security.md)).
- Band steering / "Smart Connect": **on**.
- 5 GHz channel width: 80 MHz is a common home choice (40 MHz if congested;
  160 MHz only if your environment supports it cleanly).
- 2.4 GHz channel width: keep 20 MHz to reduce overlap.
- Let the router use automatic channel selection at first, then pin channels if
  you detect interference.

## Next

- Roaming mechanics: [04-roaming.md](04-roaming.md)
- Setup steps: [setup/01-generic-setup.md](../setup/01-generic-setup.md)
- <a id="band-steering-verify"></a>Checklist:
  - Is band steering a nudge or a hard rule on your router?
  - Does your main SSID exist on both 2.4 and 5 GHz with matching security?
  - Do your IoT devices need a separate 2.4 GHz SSID?
