# Setup 03 — Validation

After configuring a unified SSID, verify that it actually behaves as one network.
Do not trust the settings page alone; test the real behavior.

## What "working" looks like

- One network name appears in the wi-fi list (not two, e.g. no separate `_5G`
  entry).
- A dual-band device connects on the faster band when close.
- Devices move between APs/bands without you reselecting a network.
- All devices can reach the internet on the unified SSID.

## Test 1 — Confirm a single SSID is broadcast

Use a Wi-Fi analyzer app on a phone:

1. Scan for networks.
2. Confirm you see **one** entry for your SSID, not `HomeWiFi` and `HomeWiFi_5G`.
3. Tap/expand the SSID: a unified network usually shows **multiple BSSIDs**
   (one per band/radio) under the same SSID.

If you see two SSIDs, cast and security likely do not match — revisit
[01-generic-setup.md](01-generic-setup.md) Steps 3–4.

## Test 2 — Confirm the device uses the right band

1. Stand next to the router/AP.
2. In your phone's Wi-Fi details (or the analyzer), check the band/frequency and
   the BSSID you are attached to.
3. A modern dual-band phone should be on **5 GHz** (or 6 GHz) when close.

If it is on 2.4 GHz:
- Confirm band steering is on ([03-band-steering.md](../docs/03-band-steering.md)).
- Toggle wi-fi off/on to force a fresh association and re-check.
- Update the phone's software.

## Test 3 — Throughput per band/location

Use a speed test at a few locations:

- Next to the AP on 5 GHz (expect the highest).
- Same spot on 2.4 GHz (expect lower).
- Far edge of coverage (expect fallback to 2.4 GHz with lower speed).

Record results. If 5 GHz is slow near the AP, check channel congestion, channel
width, and whether the device really is on 5 GHz.

## Test 4 — Roaming (multi-AP only)

Continuous ping while walking:

- **macOS/Linux:** find your gateway first (`netstat -nr | grep default`), then
  `ping <gateway>`.
- **Windows:** `ping -t <gateway>`.

Walk between APs/rooms:

- A good roam shows **0–2 lost packets** at each transition.
- Many lost packets or a long gap means sticky clients or poor tuning (see
  [04-roaming.md](../docs/04-roaming.md)).

Also watch the analyzer: the **BSSID should change** as you move to a different
AP, while the **SSID stays the same**.

## Test 5 — Device compatibility sweep

Test each device *type* you own, because clients differ:

- Modern phone/laptop (should use 5/6 GHz near the AP).
- 2.4 GHz-only IoT device (should join, possibly via an IoT SSID).
- Older laptop/tablet (should still connect on WPA2-compatible or mixed mode).
- Game console / smart TV (check latency and disconnects).

## Test 6 — Interference and channel check

With an analyzer:

- **2.4 GHz:** confirm you are on 1, 6, or 11 and that neighbors are on different
  channels.
- **5 GHz:** confirm your channel is not shared with many neighbors; try another
  80 MHz channel if throughput is poor.
- Look for co-channel and adjacent-channel overlap with your own APs.

## Test 7 — Failover/far-edge behavior

Walk to the worst-covered spot:

- The device should either fall back to 2.4 GHz with usable signal, or roam to the
  nearest AP.
- If it drops entirely, add coverage there (see
  [05-architecture.md](../docs/05-architecture.md)).

## Optional: verify steering is actually steering

Steering is invisible in most UIs. A practical check:

1. Note the band the phone uses right after a fresh association near the AP.
2. Reboot the phone's wi-fi (or the router's 2.4 GHz radio and back).
3. See whether the phone rejoins 5 GHz on its own.

If it consistently lands on 5 GHz near the AP, steering is doing its job.

## Troubleshooting pointer

If a test fails, jump to the matching symptom in
[07-troubleshooting.md](../docs/07-troubleshooting.md).

## Final validation checklist

- [ ] Only one SSID appears for the unified network.
- [ ] Multiple BSSIDs are visible under that one SSID.
- [ ] Modern devices connect on 5/6 GHz when close.
- [ ] All device types connect successfully.
- [ ] Roaming shows minimal packet loss (multi-AP).
- [ ] Throughput matches expectations per band and location.
- [ ] Channels are non-overlapping and reasonably clear.
- [ ] Guest/IoT SSIDs (if used) are isolated and present on all APs.

## Next

- Back to the [README](../README.md).
- Concepts refresher: [docs/01-concepts.md](../docs/01-concepts.md).
