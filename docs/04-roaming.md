# 04 — Roaming and the Sticky Client

Band steering picks a *band*. Roaming picks an *access point*. Together they
deliver the "one network everywhere" experience. This chapter focuses on the
second half: how clients move between APs, and why they often refuse to.

## What roaming is

Roaming is a client device leaving one BSSID and associating with another BSSID
that shares the same SSID (the ESSID). From the user's perspective, the network
name does not change; only the underlying radio does.

Example: you walk from the living room AP to the bedroom AP. The phone
reassociates from `living-room-5G` to `bedroom-5G`. Same SSID, same password, no
prompt.

## The sticky client problem

**A client decides when to roam — not the AP (in classic networks).** This is the
single most important fact. The AP cannot force most clients to leave; it can
only make staying less attractive or suggest alternatives.

A "sticky client" is a device that holds onto a far, weak AP long enough to hurt
performance — a choppy video call, slow downloads — instead of moving to a nearby
AP with a strong signal.

Why clients stick:

- Many clients roam based only on signal strength thresholds that are set
  conservatively, so they wait until the link is nearly unusable.
- Some devices have no concept of "another AP of the same network is better".
- Vendor roaming algorithms differ wildly between phone/OS versions.

## Tools to encourage good roaming

### Lower transmit power on each AP (often overlooked)

If every AP blasts at maximum power, clients see several "strong enough" APs and
stay put. Reducing TX power shrinks each AP's cell so clients are naturally
pushed toward the nearest one. This is the classic coverage-vs-capacity dial.

Rule of thumb: in a multi-AP home, lower power so that devices associate with the
*closest* AP, not the loudest distant one.

### Minimum RSSI (a.k.a. "minimum signal" / kick-out threshold)

Some APs can disconnect clients whose signal drops below a threshold, forcing
them to re-scan and find a better AP. This is effective but can be disruptive if
set too high. Start conservative (e.g. a weak threshold) and tighten gradually.

### 802.11k, 802.11v, 802.11r

These standards make roaming faster and smoother. Support varies.

- **802.11k (Radio Resource Measurement):** the AP gives the client a *neighbor
  report* — a list of nearby APs/BSSIDs — so the client does not have to scan
  blindly. Speeds up roam decisions.
- **802.11v (BSS Transition Management):** the AP can *suggest* that the client
  move to a specific BSSID. A polite nudge, not a command; clients may ignore it,
  but many modern ones comply.
- **802.11r (Fast BSS Transition / "fast roaming"):** pre-authenticates so the
  handoff between APs happens in tens of milliseconds instead of hundreds. This
  is what makes Wi-Fi calling and VoIP survive a walk across the house.

All three require support on **both** the AP *and* the client to be useful, and
they work best when a controller coordinates the APs. Stock ISP routers usually
do **not** expose k/v/r settings; see
[setup/02-isp-routers.md](../setup/02-isp-routers.md).

### Wired backhaul beats wireless backhaul

Roaming quality depends on how APs talk to each other:

- **Wired (Ethernet) backhaul:** each AP plugs into the router/switch. Fastest,
  most reliable, best roaming.
- **Wireless mesh backhaul:** nodes connect to each other over Wi-Fi. Convenient
  when you cannot run cable, but each hop adds latency and consumes airtime. A
  dedicated backhaul radio helps a lot.

Mesh systems manage roaming internally, which is why "just works" mesh kits are
popular even if individual settings are limited.

## Roaming vs band steering, side by side

| Aspect        | Band steering                          | Roaming                                   |
| ------------- | -------------------------------------- | ----------------------------------------- |
| Moves between | Bands (2.4 / 5 / 6 GHz)                | APs (BSSIDs)                              |
| Trigger       | Dual-band capability + signal quality  | Signal quality as you move                |
| Standards     | Mostly vendor behavior; k/v assist     | 802.11k/v/r (when supported)              |
| User impact   | Faster link where available            | No drop while walking                     |
| Requires      | Unified SSID                           | Unified SSID across APs                   |

## Practical tuning order

1. Get a unified SSID working on all bands/APs ([setup/01-generic-setup.md](../setup/01-generic-setup.md)).
2. Use wired backhaul where possible.
3. Reduce AP transmit power so cells overlap only slightly.
4. If your hardware supports it, enable 802.11k/v/r and set a conservative
   minimum-RSSI threshold.
5. Test by walking around on a call or continuous ping.

## Testing roaming

- Run a continuous `ping` to the router gateway from a laptop and walk around.
  A good roam shows one or two lost packets; a bad one shows many.
- On a phone, start a video call and walk between rooms; listen for gaps.
- Use a Wi-Fi analyzer app to watch the BSSID your device is attached to change
  as you move.

## Next

- Architecture choices: [05-architecture.md](05-architecture.md)
- Troubleshooting sticky clients: [07-troubleshooting.md](07-troubleshooting.md)
- <a id="roaming-verify"></a>Checklist:
  - Do you have more than one AP? If so, is backhaul wired?
  - Is transmit power tuned down so cells do not overlap too much?
  - Does your hardware expose k/v/r? If not, is roaming still acceptable?
