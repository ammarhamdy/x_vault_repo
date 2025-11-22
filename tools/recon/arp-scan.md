

`arp-scan` is a command-line tool used for network discovery by sending ARP packets and listing all active devices on a local network. 

It’s useful for identifying devices on your LAN (Local Area Network).

---

**discover devices:**
```sh
arp-scan --interface=eth0 192.168.1.0/24
```

**List all interfaces:**
```
arp-scan --interface=eth0 --localnet
```

**Scan specific IPs:**
```
sudo arp-scan 192.168.1.10 192.168.1.11
```


---

# Lookup databases for arp-scan

`ieee-oui.txt` and `mac-vendor.txt` On Ubuntu:
```
ieee-oui.txt      /usr/share/arp-scan/ieee-oui.txt
mac-vendor.txt    /etc/arp-scan/mac-vendor.txt
```

Those two files are basically **lookup databases** that `arp-scan` uses to map MAC addresses to vendor/manufacturer names.

## `ieee-oui.txt`
- This is a copy of the official **IEEE OUI (Organizationally Unique Identifier)** database.
- Each entry maps the **first 24 bits (first 3 bytes)** of a MAC address to the organization that registered it.

**Example content:**
```sh
# Start of IEEE IAB registry data
#
0050C27D5       DEUTA-WERKE GmbH
40D85511C       DEUTA-WERKE GmbH
40D8551A1       KRONOTECH SRL
0050C2CF9       Elbit Systems of America
0050C2F6B       Algodue Elettronica Srl
0050C21FA       SP Controls, Inc
0050C2811       Open System Solutions Limited
....
```
If `arp-scan` sees a device with MAC `0050C2F6B`, it will display **`Algodue Elettronica Srl`** as the vendor.

### Update vendor files
To fetch the latest IEEE OUI database:
```
sudo get-oui
```

## `mac-vendor.txt`
- This is a supplementary تكميلي file specific to `arp-scan`.
- It contains **additional or corrected vendor mappings** not present in the `IEEE OUI` database.

**Example content:**
```sh
# From RFC 2338: 00-00-5E-00-01-{VRID}
00:00:5e:00:01  VRRP (last octet is VRID)

# Microsoft WLBS (Windows NT Load Balancing Service)
# http://www.microsoft.com/technet/prodtechnol/acs/reskit/acrkappb.mspx
02:bf   Microsoft WLBS (last four octets are IP address)

# Cisco HSRP (Hot Standby Routing Protocol)
# 00-00-0c-07-ac-XX, where XX is the HSRP group number (0 to 255)
00:00:0c:07:ac  HSRP (last octet is group number)

# Ethernet broadcast address
ff:ff:ff:ff:ff:ff       Broadcast
```
It’s often community-maintained to cover smaller vendors, virtual interfaces, or updates faster than IEEE publishes them.


## Why they matter

- Without these files, `arp-scan` will still show you the **IP and MAC addresses**, but you won’t see the **manufacturer/vendor** info.

- With them, you can quickly identify devices on the network (e.g., “that’s a Samsung phone, that’s a Cisco switch”).


##  Use `arp-scan` with specific Lookup databases

**Tell `arp-scan` where the files are:**
```sh
sudo arp-scan -I wlo1 192.168.1.1   --ouifile=/usr/share/arp-scan/ieee-oui.txt   --macfile=/etc/arp-scan/mac-vendor.txt
```

If you want `arp-scan` create another place, you can create symlinks:

```sh
sudo mkdir -p /usr/local/share/arp-scan
```

```sh
sudo ln -s /usr/share/arp-scan/ieee-oui.txt /usr/local/share/arp-scan/ieee-oui.txt
```

```sh
sudo ln -s /etc/arp-scan/mac-vendor.txt /usr/local/share/arp-scan/mac-vendor.txt
```

