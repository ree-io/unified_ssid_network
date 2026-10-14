# 01 — Core Concepts

Before setting anything up, it helps to be precise about the words. "SSID" is
used loosely in everyday conversation, but three different identifiers are in
play: SSID, BSSID, and ESSID.

## SSID: the network name

An **SSID** (Service Set Identifier) is the human-readable wi-fi network name —
for example `HomeWiFi`. It is up to 32 characters. When you open your phone's
wi-fi list and see `HomeWiFi`, you are looking at an SSID.

A single physical radio can broadcast more than one SSID (for example, your main
network plus a guest network).

## BSSID: one radio's identity

A **BSSID** (Basic Service Set Identifier) is the MAC address of a specific
radio/access point broadcasting an SSID. It looks like `a4:2b:8c:11:22:33`.

This is the number your device actually associates with. When you connect to
`HomeWiFi`, the phone picks a particular BSSID behind the scenes.

Key point: **one SSID can map to many BSSIDs.** A dual-band router broadcasting
`HomeWiFi` on 2.4 GHz and 5 GHz has two BSSIDs for the same SSID. Add a third
AP and there are more.

```
SSID: HomeWiFi
├── BSSID a4:2b:8c:11:22:33   (2.4 GHz radio)
├── BSSID a4:2b:8c:11:22:34   (5 GHz radio)
└── BSSID b8:1d:aa:44:55:66   (5 GHz radio on a second AP)
```

## ESSID: the network as a whole

An **ESSID** (Extended Service Set Identifier) is the SSID value shared by
multiple BSSIDs that belong to the same logical network. In practice, when people
say "SSID" for a network spanning several APs, they usually mean the ESSID.

For this guide, the takeaway is simple: a **unified SSID network** is a set of
BSSIDs that share one SSID and one set of security settings, so client devices
see and treat them as one network.

## What "unified" means

Unifying means making these consistent:

1. **Network name** — the same SSID on every band and every AP.
2. **Security** — the same password and encryption type (usually WPA2/WPA3).
3. **Band and AP membership** — devices are allowed to connect to any of them.

When all three match, a phone that was connected on the 5 GHz radio in the living
room can reassociate to the 5 GHz radio in the bedroom — or fall back to 2.4 GHz
at the far end of the house — and from the user's point of view, nothing "changed
networks".

If any of the three differ, you have effectively created two networks. A very
common mistake is giving 2.4 GHz and 5 GHz different names (`HomeWiFi` and
`HomeWiFi_5G`). That is a *split* SSID, not a unified one, and devices will not
move between them automatically.

## Unified SSID is the goal; these are the tools

| Term          | Relationship to unified SSID                                                   |
| ------------- | ------------------------------------------------------------------------------ |
| Band steering | A technique to push dual-band clients onto the faster band while keeping one SSID |
| Roaming (k/v/r) | Protocols that help clients move between APs/BSSIDs quickly                 |
| Mesh          | A way to extend coverage with wireless backhaul, usually shown as one SSID    |

You can have a unified SSID without band steering (devices just choose for
themselves). You can have band steering only make sense *because* the SSID is
unified. And a mesh system typically presents a unified SSID by design.

## Single SSID vs split SSID

**Single/unified SSID**

- One name, e.g. `HomeWiFi`, on both bands.
- Devices pick a band themselves (or get steered).
- Roaming between APs is transparent.
- Downside: older or picky devices sometimes cling to 2.4 GHz, and you cannot
  force a specific band from the client side.

**Split SSID**

- Two names, e.g. `HomeWiFi` and `HomeWiFi_5G`.
- You manually choose the band per device — useful for troubleshooting or for
  devices that steer badly.
- No automatic movement between bands.
- Often used as a temporary diagnostic step.

## A quick mental model

Think of the SSID as a *business name* and BSSIDs as *branches* of that business.
Your device walks into whichever branch is closest/strongest. A unified SSID
means every branch has the same name and accepts the same membership card (your
password). Band steering is a greeter at the door pointing fast clients to the
express lane (5 GHz) and slow ones to the regular lane (2.4 GHz).

## Next

- Why and when to unify: [02-use-cases.md](02-use-cases.md)
- The band-steering detail: [03-band-steering.md](03-band-steering.md)
- <a id="concepts-verify"></a>Verify you understand:
  - Can you explain why `HomeWiFi` and `HomeWiFi_5G` is *not* unified?
  - How many BSSIDs does a dual-band router broadcasting one SSID create?
  - Which is the goal and which is a technique: unified SSID or band steering?
