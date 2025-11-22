
https://www.kali.org/tools/mdk4/

---

This package contains a proof-of-concept tool to exploit common [[EEE 802.11 protocol]] protocol weaknesses.

`MDK4` is the **newer, more stable version** of `MDK3`. 

It’s widely used in wireless security testing and research.

---

# Installation
```sh
sudo apt install mdk4
```

# Prepare Your Wi-Fi Adapter
Switch your adapter into **monitor mode** (replace `wlo1` with your interface):

```sh
sudo ip link set wlo1 down
```
- **`ip link`** → tool for managing network interfaces.
- **`set wlo1 down`** → turns the Wi-Fi interface **off temporarily** (like disabling it).
- Why? Because you can only change the mode of a Wi-Fi card when it’s **down**.

```sh
sudo iw dev wlo1 set type monitor
```
- **`iw`** → modern command for configuring wireless devices (replaces old `iwconfig`).
- **`dev wlo1`** → target device (your Wi-Fi card).
- **`set type monitor`** → changes the mode from ==_managed_== (normal Wi-Fi client mode) to ==_monitor== mode_.
+ **Monitor Mode** -> the Wi-Fi card can capture **all packets in the air**, not just those addressed to it.

```sh
sudo ip link set wlo1 up
```
- Brings the Wi-Fi interface **back up** after changing the mode.
- Now your `wlo1` is alive again, but in **monitor mode** instead of managed mode.

# Common `MDK4` Modes
`MDK4` has multiple attack/test modes. Here are the most useful ones:
+ Deauthentication
+ Beacon Flood (Fake Access Points)
+ Authentication Flood
+ Probe Request Flood
+ Michael MIC Exploits (`TKIP`/`WPA1`)

# Deauthentication (Disassociation Flood)
Forces clients to disconnect:
```sh
sudo mdk4 wlo1 d
```
Options:
- `-c <channel>` → target channel
- `-t <MAC>` → target a specific AP

# Beacon Flood (Fake Access Points)
Creates fake `APs` to test client behavior:
```sh
sudo mdk4 wlo1 b -f ssid-list.txt
```
Where `ssid-list.txt` contains `SSIDs`, one per line.

# Authentication Flood
Spams authentication requests to an AP:
```sh
sudo mdk4 wlo1 a -t <AP_MAC>
```

# Probe Request Flood
Spams (رسائل إلكترونية مزعجة) ___probe requests___ with random or chosen `SSIDs`:
```sh
sudo mdk4 wlo1 p
```
+ A probe request is ==a wireless management frame sent by a Wi-Fi client device to discover available networks, either by searching for a specific network (`SSID`) or any network in the vicinity==.

# Michael MIC Exploits (`TKIP`/`WPA1`)
Legacy exploit testing (almost **obsolete**):
```sh
sudo mdk4 wlo1 m
```

