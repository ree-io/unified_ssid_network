# Setup 00 — Prerequisites

Before changing anything, gather access and information. Ten minutes here saves an
hour of confusion.

## What you need

- **Admin access to your router.** The default gateway IP (often `192.168.1.1` or
  `192.168.0.1`), and the admin username/password.
- **Wi-Fi credentials** for the current network (so you can reconnect after
  changing settings).
- **A wired device if possible** — a laptop connected by Ethernet is the safest
  way to reconfigure wi-fi, because you will not lose your connection mid-change.
- **A phone/tablet** with a Wi-Fi analyzer app for testing.
- **Pen and paper or a notes file** to record settings.

## Find your router's admin address

On a computer connected to the network:

- **Windows:** `ipconfig` → look for "Default Gateway".
- **macOS/Linux:** `netstat -nr | grep default` or `ip route` → gateway address.

Then open `http://<gateway-ip>` in a browser. Many ISP routers also print their
admin address and credentials on a sticker on the device.

> Note: these commands are read-only and safe. Running them does not change any
> network configuration.

## Find the admin credentials

- **On the device sticker:** look for "admin", "web access", or "GUI" login.
- **ISP-provided:** sometimes printed on the installation receipt, or provided
  via the ISP's app/account portal.
- **Common defaults:** vary by brand and model — use the sticker or manual rather
  than guessing. Repeated failed logins can lock the account.

If the credentials are locked, do not attempt recovery procedures that could
disrupt service. Instead, consider adding your own AP/router in bridge mode
(see [02-isp-routers.md](02-isp-routers.md)).

## Record your current settings first

Before changing anything, note:

- Current SSID name(s) — there may be separate 2.4 and 5 GHz names.
- Current security mode (WPA2/WPA3, PSK).
- Wi-Fi password.
- Whether band steering / "Smart Connect" is on or off.
- The router's LAN IP and subnet (e.g. `192.168.1.1/24`).
- Whether the ISP router also does DHCP/NAT (it almost always does).

This baseline lets you roll back if something breaks.

## Know what your hardware supports

Feature availability varies enormously. Check for these in the admin UI or manual:

| Feature                          | Why it matters                       |
| -------------------------------- | ------------------------------------ |
| Single/merged SSID option        | Baseline for unification             |
| Band steering / Smart Connect    | The core steering feature            |
| Per-band SSID names              | Needed if you must split bands       |
| WPA2/WPA3 selectable             | Security compatibility               |
| Guest network                    | Isolation for visitors               |
| AP / bridge mode                 | Required when adding your own router |
| 802.11k/v/r                      | Better roaming (rarely on ISP gear)  |

Stock ISP routers frequently lock or hide these. If a feature you need is
missing, the practical solution is usually to **add your own AP/router in bridge
mode** and manage the unified SSID there.

## Safety rules

1. Do not change the router's WAN/PPPoE/fiber settings — those carry your internet
   service and a mistake can take you offline.
2. Only change **Wi-Fi / LAN / wireless** settings for this task.
3. Reconfigure from a wired connection where possible.
4. Keep the old wi-fi password until the new one is confirmed working.
5. Change one thing at a time and test after each change.

## Decision: stock router only, or add hardware?

- If the stock router can broadcast one SSID across its bands and enable band
  steering → start there ([01-generic-setup.md](01-generic-setup.md)).
- If you need better coverage or roaming → plan to add an AP or mesh node, in
  bridge/AP mode ([02-isp-routers.md](02-isp-routers.md)).

## Next

- [01-generic-setup.md](01-generic-setup.md) — vendor-neutral setup steps.
- <a id="prereq-verify"></a>Checklist:
  - Gateway IP found?
  - Admin login confirmed working?
  - Current settings recorded?
  - Hardware feature support identified?
