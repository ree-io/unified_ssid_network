# Glossary

Terms used throughout this repository, in roughly the order you will encounter
them.

- **SSID (Service Set Identifier):** the human-readable wi-fi network name, up to
  32 characters, e.g. `HomeWiFi`.
- **BSSID (Basic Service Set Identifier):** the MAC address of a specific radio
  broadcasting an SSID. Your device associates with a BSSID, not an SSID.
- **ESSID (Extended Service Set Identifier):** the SSID value shared by multiple
  BSSIDs belonging to the same logical network. Practically, "the network" when
  spanning several APs.
- **Unified SSID network:** a set of BSSIDs sharing one SSID and one set of
  security settings, so clients treat them as one network.
- **Split SSID:** two different network names for the bands, e.g. `HomeWiFi` and
  `HomeWiFi_5G`. No automatic movement between bands.
- **AP (Access Point):** a device that provides wi-fi access to the network. A
  router is often also an AP.
- **Access Point / Bridge mode:** a mode where a device only provides wi-fi/LAN
  access and does not route or run its own DHCP server. Required when adding an
  AP behind another router.
- **Router mode:** a mode where the device routes between networks and typically
  runs its own DHCP and NAT.
- **DHCP (Dynamic Host Configuration Protocol):** the service that hands out IP
  addresses to devices. Only one DHCP server should exist on a LAN.
- **NAT (Network Address Translation):** the router feature that lets local
  devices share one public IP. Two layers of NAT ("double-NAT") cause problems.
- **Double-NAT:** two devices both doing NAT/routing, often from stacking routers.
  Breaks port forwarding and some services.
- **2.4 GHz:** the frequency band with longer range and better wall penetration
  but lower speed and higher congestion.
- **5 GHz:** the band with higher speed but shorter range and moderate
  congestion. Preferred for modern devices near an AP.
- **6 GHz:** the newest band (Wi-Fi 6E/7), fastest and least congested, with the
  shortest range.
- **Channel:** a slice of a band, e.g. 1/6/11 on 2.4 GHz. Overlapping channels
  cause interference.
- **Channel width:** how wide the channel is (20/40/80/160 MHz). Wider can mean
  faster but more collision-prone and less spectrum-efficient.
- **RSSI (Received Signal Strength Indicator):** a measure of signal strength,
  usually negative dBm; closer to 0 is stronger.
- **Co-channel interference:** two radios on the same channel sharing airtime,
  slowing both.
- **Band steering:** encouraging dual-band clients to use the better band
  (usually 5/6 GHz) while keeping a single unified SSID. A nudge, not always a
  guarantee.
- **Smart Connect / Unified Band:** vendor names for combined-band / band
  steering behavior.
- **Probe suppression:** an AP holding back its 2.4 GHz probe response to nudge a
  dual-band client toward 5 GHz.
- **Roaming:** a client moving from one BSSID to another under the same SSID.
- **Sticky client:** a device that stays on a distant/weak AP instead of moving
  to a nearer one.
- **Minimum RSSI / kick-out threshold:** a setting that disconnects clients whose
  signal falls below a threshold, forcing them to re-scan.
- **802.11k:** Radio Resource Measurement — the AP supplies a neighbor report so
  clients roam faster.
- **802.11v:** BSS Transition Management — the AP suggests a client move to a
  better BSSID.
- **802.11r:** Fast BSS Transition ("fast roaming") — pre-authenticates so AP
  handoffs happen in milliseconds.
- **Backhaul:** the connection between APs or nodes (wired Ethernet, wireless
  mesh, MoCA, powerline).
- **Mesh:** a multi-node system with (usually) a wireless backhaul, presented as
  one SSID.
- **Controller:** a central manager coordinating many APs (roaming, channels,
  power, policy). Controllerless APs are configured individually.
- **Enterprise mode / 802.1X:** per-user authentication via a RADIUS server,
  instead of a shared password.
- **PSK (Pre-Shared Key):** the wi-fi password used in WPA2/WPA3-Personal.
- **WPA2-Personal (AES):** the widely compatible password-based security mode.
- **WPA3-Personal (SAE):** the newer, stronger password-based mode; not all
  devices support it.
- **WPA2/WPA3 transition (mixed) mode:** allows both, for compatibility during
  migration.
- **TKIP:** an obsolete encryption method; avoid it. Prefer AES/CCMP.
- **WEP:** a long-broken encryption standard; never use it.
- **WPS (Wi-Fi Protected Setup):** a push-button/PIN onboarding feature with known
  weaknesses; disable it.
- **AP / client isolation:** a setting preventing wireless clients from talking to
  each other; used on guest and IoT networks.
- **Guest network:** a separate SSID for visitors, ideally isolated from the main
  LAN.
- **IoT (Internet of Things):** smart devices (plugs, cameras, sensors), often
  2.4 GHz-only and often the weakest security link.
- **VLAN (Virtual LAN):** a way to logically separate traffic on the same
  physical network, e.g. putting IoT on its own segment.
- **ONT (Optical Network Terminal):** the fiber modem the ISP installs; may also
  act as a router/AP.
- **PPPoE:** the authentication method some ISPs use on the WAN; do not change it.
- **TR-069:** the remote-management protocol ISPs use to provision and update
  customer routers; often why settings get reset remotely.
- **MLO (Multi-Link Operation):** a Wi-Fi 7 feature where a device uses multiple
  bands/links at once, improving throughput and reliability.
