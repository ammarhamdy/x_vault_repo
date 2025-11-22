
# Check if you WiFi card support AP (Access point) mode

```sh
iw list | grep "AP"
```

---
# Overview

🖧 `hostapd` creates the Wi-Fi signal → 📱 devices connect → 💡 `dnsmasq` assigns them IPs and routes DNS → 🌐 internet sharing works.

---

# `hostapd`

==The software that makes your computer behave like a Wi-Fi router.==

The command **`hostapd`** stands for **Host Access Point Daemon (شيطان)** — it’s the program that actually **turns your Linux machine (like Ubuntu) into a Wi-Fi hotspot (access point)**.

**What `hostapd` does:**

- **Reads your configuration file** (e.g. `/etc/hostapd/hostapd.conf`)  
    That file defines things like:
    - `ssid` → the name of your hotspot
    - `wpa_passphrase` → the Wi-Fi password
    - `channel` → which Wi-Fi channel to use
    - `interface` → which network interface (e.g. `wlan0`, `wlp2s0`)
        
- **Configures the wireless interface** to broadcast that SSID and accept connections.
    
- **Handles Wi-Fi authentication and encryption**, e.g. `WPA2`, `WPA3`.
    
- **Coordinates with `dnsmasq` or another DHCP server** to give IP addresses to clients that connect.

---

## Installation
```
sudo apt install hostapd
```

## Stop & disable
```sh
sudo systemctl stop hostapd
sudo systemctl disable hostapd
```

## Common commands for hostapd

| Command                                  | Description                      |
| ---------------------------------------- | -------------------------------- |
| `sudo hostapd /etc/hostapd/hostapd.conf` | Start hotspot manually           |
| `sudo systemctl start hostapd`           | Start it as a background service |
| `sudo systemctl enable hostapd`          | Auto-start on boot               |
| `sudo systemctl status hostapd`          | Check if it’s running            |
| `sudo systemctl stop hostapd`            | Stop the hotspot                 |

## Create config files

Create configuration file `/etc/hostapd/hostapd.conf`:
```less
interface=wlp2s0
driver=nl80211
ssid=UbuntuHotspot
hw_mode=g
channel=6
wmm_enabled=1
auth_algs=1
wpa=2
wpa_passphrase=yourpassword
wpa_key_mgmt=WPA-PSK
rsn_pairwise=CCMP
```

## Point `hostapd` to this file:

```sh
sudo sed -i 's|#DAEMON_CONF=""|DAEMON_CONF="/etc/hostapd/hostapd.conf"|' /etc/default/hostapd
```


---
# `dnsmasq`


**`dnsmasq`** is a **lightweight DNS and DHCP server** commonly used on Linux systems (including Ubuntu).  
It’s often paired with `hostapd` when creating a Wi-Fi hotspot.

>`dnsmasq` gives connected devices their IP addresses and helps them resolve domain names

**What It Does**

When you run `dnsmasq`, it performs two main jobs:

1. **DHCP (Dynamic Host Configuration Protocol):**
    It automatically gives out IP addresses to devices that connect to your hotspot.  
    Example: Your phone connects → `dnsmasq` assigns it `192.168.50.10`.
    
2. **DNS (Domain Name System):** 
    It resolves domain names (like `google.com`) to IP addresses.  
    It can forward those requests to your upstream DNS servers (e.g. Google’s `8.8.8.8`).

---

**When you turn your Ubuntu into a Wi-Fi hotspot:**

- **`hostapd`** = creates the Wi-Fi network and handles authentication
    
- **`dnsmasq`** = gives connected devices IPs + internet access via DNS & DHCP

---
## Command command for dnsmasq

| Command                                             | Description                                                       |
| --------------------------------------------------- | ----------------------------------------------------------------- |
| `sudo systemctl start dnsmasq`                      | Start the dnsmasq service                                         |
| `sudo systemctl stop dnsmasq`                       | Stop it                                                           |
| `sudo systemctl restart dnsmasq`                    | Restart (useful after editing config)                             |
| `sudo systemctl status dnsmasq`                     | Check if it’s running                                             |
| `sudo dnsmasq --no-daemon --log-queries --log-dhcp` | Run in foreground with debug logging (useful for troubleshooting) |

## Typical Configuration

```
# The Wi-Fi interface used for the hotspot
interface=wlp2s0

# DHCP range and lease time
dhcp-range=192.168.50.10,192.168.50.100,12h   

domain-needed
bogus-priv
```
- “Manage DHCP on interface `wlp2s0`.”
- “Give IPs between `192.168.50.10` and `192.168.50.100`.”
- “Leases last for 12 hours.”

## Verify it’s working
```sh
sudo journalctl -u dnsmasq -f
```
You’ll see log messages when devices connect and get IP addresses.


---

# Create hotspot


When you turn your Ubuntu machine into a Wi-Fi hotspot, two main background services cooperate:

| Component     | Role                                                                    | Analogy                              |
| ------------- | ----------------------------------------------------------------------- | ------------------------------------ |
| **`hostapd`** | Creates and manages the Wi-Fi access point (SSID, password, encryption) | The _Wi-Fi transmitter/router radio_ |
|**`dnsmasq`**|Assigns IP addresses and handles DNS for connected devices|The _DHCP & DNS server_|

---

## Backup for `/etc/dnsmasq.conf`
```sh
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
sudo nano /etc/dnsmasq.conf
```
Add:
```
interface=wlp2s0
dhcp-range=192.168.50.10,192.168.50.100,12h
```

## Step 1 — `hostapd` starts
You start it manually or via `systemd`:
```sh
sudo systemctl start hostapd
```
- Configures your Wi-Fi adapter into **AP mode**
- Starts broadcasting your **SSID** (Wi-Fi name)
- Accepts connections from client devices
- Handles **WPA2/WPA3 authentication**
+ Once a device connects successfully (authenticates), it’s _associated_ — but it still has **no IP address** yet.

## Step 2 — `dnsmasq` assigns IPs
You start `dnsmasq`:
```sh
sudo systemctl start dnsmasq
```
- Detects the connected devices on the same interface
- Assigns IPs (e.g., `192.168.50.10`, `192.168.50.11`, etc.)
- Maintains a small DHCP lease table
- Forwards DNS queries (e.g., `google.com`) to your upstream DNS (e.g., `8.8.8.8`)
- Now devices can communicate with your Ubuntu hotspot — but they still can’t reach the **internet** yet unless we forward traffic.

## Step 3 — Ubuntu shares its internet
You add a NAT (Network Address Translation) rule with `iptables`:
```sh
sudo iptables -t nat -A POSTROUTING -o <internet_interface> -j MASQUERADE
```
- If your Ubuntu connects to the internet via Wi-Fi → replace `<internet_interface>` with `wlp2s0`
- If it uses Ethernet → replace with `eth0`
- This makes Ubuntu **act like a router** — packets from connected devices are “masqueraded” (rewritten) to go through your Ubuntu’s own IP.

## Step 4 — Internet sharing works
Now the full flow looks like this:
```sh
[Phone/Laptop] --Wi-Fi--> [Ubuntu hostapd AP]
           ↓
   (gets IP via dnsmasq)
           ↓
   (DNS via dnsmasq)
           ↓
   (traffic NATed via iptables)
           ↓
       Internet 🌍
```

## Example Configuration Summary

**`/etc/hostapd/hostapd.conf`**
```
interface=wlp2s0
driver=nl80211
ssid=UbuntuHotspot
hw_mode=g
channel=6
wmm_enabled=1
auth_algs=1
wpa=2
wpa_passphrase=mysecret123
wpa_key_mgmt=WPA-PSK
rsn_pairwise=CCMP
```

**`/etc/dnsmasq.conf`**
```sh
interface=wlp2s0
dhcp-range=192.168.50.10,192.168.50.100,12h
```

**NAT rule**
```sh
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

