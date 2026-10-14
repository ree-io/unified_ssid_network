# Unified SSID Network

## TL;DR version

Instead of having 2 distinct SSIDs, have only 1. When you're far away from the wifi, your device automatically uses 2.4 Ghz.  
When near, it will also automatically switch to 5 Ghz (with the help of band steering).

> “Why waste time say lot word when few word do trick” - Kevin, The Office

## More words version..

A practical, vendor-neutral guide to **unified SSID networks** — running a single
wi-fi network name (SSID) across multiple frequency bands and, where applicable,
multiple access points, so your devices move between them without you managing a
separate network for each one.

This repo teaches the concept, why it matters, the related technique of **band
steering**, and how to set it up on typical home hardware — including the
stock routers provided by Philippine ISPs such as **PLDT Home Fibr**, **Globe At
Home**, and **Converge**.

## Who this is for

- Home-lab and prosumer users who want one clean wi-fi network instead of two or
  three.
- Anyone whose house has dead spots and wants roaming to "just work".
- Users of ISP-provided routers who want to know what the stock firmware can and
  cannot do.

This is written at an **intermediate** level: you should be comfortable logging
into a router's admin page and changing wi-fi settings. Deep RF theory is out of
scope, but the important protocols are explained.

## What a unified SSID network actually is

Your phone sees one network name, e.g. `HomeWiFi`. Behind that name there may be
several radios:

- a 2.4 GHz radio (longer range, slower),
- one or more 5 GHz radios (faster, shorter range),
- possibly a 6 GHz radio on Wi-Fi 6E/7 gear,
- possibly several access points around the house.

A **unified SSID** means all of these broadcast the *same* network name and
security settings, so the device treats them as one network it can move within.
That is what makes seamless walking-around-the-house and automatic picking of the
better band possible.

A unified SSID is the *goal*; **band steering** and **fast roaming** are the
*techniques* that make it work well. They are related, not synonyms.

## Learning path

Read in order if this is new to you:

1. [README.md](README.md) — you are here.
2. [docs/01-concepts.md](docs/01-concepts.md) — SSID, BSSID, ESSID and what "unified" means.
3. [docs/02-use-cases.md](docs/02-use-cases.md) — when and why to unify.
4. [docs/03-band-steering.md](docs/03-band-steering.md) — 2.4/5/6 GHz and steering.
5. [docs/04-roaming.md](docs/04-roaming.md) — sticky clients, 802.11k/v/r.
6. [docs/05-architecture.md](docs/05-architecture.md) — single AP vs mesh vs wired APs.
7. [docs/06-security.md](docs/06-security.md) — WPA3, guest and IoT separation.
8. [docs/07-troubleshooting.md](docs/07-troubleshooting.md) — when it misbehaves.

Then set it up:

- [setup/00-prerequisites.md](setup/00-prerequisites.md)
- [setup/01-generic-setup.md](setup/01-generic-setup.md)
- [setup/02-isp-routers.md](setup/02-isp-routers.md) — PLDT / Globe / Converge
- [setup/03-validation.md](setup/03-validation.md)

Reference:

- [glossary.md](glossary.md)

## Repository layout

```
README.md                Overview and table of contents
docs/                    Concept chapters (01-07)
setup/                   Step-by-step setup guides
glossary.md              Terms used across the repo
```

## Quick reference: unified SSID vs band steering vs roaming

| Concept          | What it is                                            | Why it matters                                  |
| ---------------- | ----------------------------------------------------- | ----------------------------------------------- |
| Unified SSID     | Same network name + security across all radios/APs    | One network to join; devices can move freely    |
| Band steering    | Nudging dual-band clients toward the best band        | Keeps 2.4 GHz free for slow/legacy devices      |
| Fast roaming     | 802.11k/v/r helping clients switch APs quickly        | Smooth calls/video while walking                |
| Mesh             | Multiple nodes with a wireless backhaul               | Covers a home without pulling cable everywhere  |

> Note: exact menu names differ between router brands, models, and firmware
> revisions. The setup guides describe the settings to look for and note where
> labels commonly vary. Always verify against your specific device's manual.
