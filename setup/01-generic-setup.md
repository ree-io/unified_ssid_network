# Setup 01 — Generic Setup (Vendor-Neutral)

This is the vendor-neutral procedure to create a unified SSID network. Apply it
to any router or AP; brand-specific quirks for Philippine ISP routers are in
[02-isp-routers.md](02-isp-routers.md).

Throughout, menu names are described generically with common aliases in
parentheses. Exact labels differ by brand and firmware.

## Step 1 — Log in to the router/AP

1. Connect to the network (wired preferred).
2. Open the admin page at the gateway address.
3. Log in with admin credentials.

## Step 2 — Confirm both bands exist and are enabled

Go to the **Wireless** (Wi-Fi / Wireless Settings) section. You should see:

- a **2.4 GHz** radio section,
- a **5 GHz** radio section (and possibly a 6 GHz section on newer gear).

Ensure both are enabled. Record the current SSID names for each band.

## Step 3 — Match the SSID across bands

This is the heart of unification.

1. In the **2.4 GHz** settings, note the SSID (e.g. `HomeWiFi_2.4G`).
2. Set the **5 GHz** SSID to the *exact same name*. Case, spaces, and punctuation
   must match exactly.
3. Set a single, shared SSID you want to use, e.g. `HomeWiFi`, on both bands.
4. Save/Apply.

Read the following aloud before moving on: *the two bands must have the same
SSID.* A difference of even one character creates two networks.

> Some firmwares offer a single "SSID" field that applies to all bands when a
> "Smart Connect" or "Band Steering" toggle is on. In that case you only set the
> name once. If you see separate fields, set both manually.

## Step 4 — Match the security settings across bands

For each band, set identical values:

- **Security mode:** WPA2/WPA3 mixed (transition) is a good default. Use
  WPA2-Personal (AES) if you have stubborn legacy devices, or WPA3-only only if
  all devices support it.
- **Password/PSK:** the exact same password on both bands.
- **Encryption:** AES/CCMP. Avoid TKIP and WEP.

Mismatched security between bands is a classic reason a device connects to one
band but not the other.

## Step 5 — Enable band steering (if available)

Look for a toggle named **Band Steering**, **Smart Connect**, **Band
Balancing**, or **Auto Band**. Turn it **on**.

- If it is a single combined SSID feature, enabling it may merge the bands for
  you — re-check the SSID and security in Steps 3–4.
- If aggressive steering causes one device to fail to connect, note which device
  and consider a separate SSID for it (Steps 9–10).

See [../docs/03-band-steering.md](../docs/03-band-steering.md) for the mechanism.

## Step 6 — Choose channels and widths

- **2.4 GHz:** width **20 MHz**. Use only channels **1, 6, or 11** and pick the
  least crowded (use a Wi-Fi analyzer in your area).
- **5 GHz:** width **80 MHz** is a good home default. Use 40 MHz if the area is
  congested; 160 MHz only if the airspace is clean.
- **6 GHz:** let it auto-select; it is usually uncongested.
- Start with **automatic** channel selection, then pin the channel once you know
  what is clean.

## Step 7 — (If adding an AP) Put it in AP/bridge mode

When adding a second access point:

1. Connect it by Ethernet to the main router/switch where possible.
2. Log in to the AP's admin page.
3. Set it to **Access Point** / **Bridge** mode (not Router mode).
4. **Disable its DHCP server** so only the main router hands out IP addresses.
5. Configure the *same* SSID, password, and security as the main network.
6. Set its LAN IP within the main subnet but outside the DHCP pool, to avoid
   conflicts.

This creates additional BSSIDs under the same ESSID and enables real roaming.

## Step 8 — (If using a router behind the ISP router) avoid double-NAT

Prefer AP/bridge mode. If you must use your own router as the main router:

- Put the ISP device in **bridge mode** if the ISP allows it, **or**
- Keep the ISP device as the router and use your device only as an AP.

See [../docs/05-architecture.md](../docs/05-architecture.md).

## Step 9 — (Optional) Add a guest SSID

1. Enable the **Guest Network**.
2. Give it its own SSID and password.
3. Enable **client/AP isolation**.
4. Ensure the guest SSID exists on **all** APs with the same settings.
5. Optionally rate-limit it.

## Step 10 — (Optional) Add a 2.4 GHz IoT SSID

For devices that only work on 2.4 GHz or ignore band steering:

1. Create an SSID (e.g. `HomeIoT`) on the **2.4 GHz radio only**.
2. Use **WPA2-AES** for maximum compatibility.
3. Onboard each IoT device to that SSID.
4. Isolate it from trusted devices if your router supports VLANs.

## Step 11 — Save and reconnect

1. Apply all changes.
2. Your devices will disconnect. Reconnect using the unified SSID and password.
3. Run the validation steps in [03-validation.md](03-validation.md).

## Step 12 — Tune roaming (multi-AP only)

- Lower each AP's **transmit power** so cells overlap only slightly.
- If supported, enable **802.11k/v/r**.
- Set a conservative **minimum RSSI** threshold if available.
- Test by walking around on a call or continuous ping.

## Rollback

If something breaks and you lose access, reconnect using the *old* SSID and
password (if you kept them unchanged) or reset the router to defaults and
reconfigure from your recorded baseline.

## Next

- ISP-specific guidance: [02-isp-routers.md](02-isp-routers.md)
- Validate: [03-validation.md](03-validation.md)
- <a id="generic-setup-verify"></a>Checklist:
  - Same SSID on every band?
  - Same security and password on every band/AP?
  - Band steering on (if available)?
  - Extra APs in AP/bridge mode with DHCP off?
  - Channels/widths chosen sensibly?
