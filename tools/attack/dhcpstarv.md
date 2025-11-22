
that’s a small attack/testing tool specifically used for **DHCP starvation attacks**.

---
# Installation
```sh
sudo apt install dhcpstarv
```

# What is `dhcpstarv`?
- `dhcpstarv` is a penetration testing tool that floods a DHCP server with **`DHCPDISCOVER`** requests.
- Each request uses a **spoofed MAC address**, tricking the DHCP server into leasing all available IPs.
- Once the pool is empty, **legitimate clients cannot get an IP** → denial of service.

# How `dhcpstarv` Works
1. Sends continuous **`DHCPDISCOVER`** messages.
2. Spoofs the **Client Hardware Address (`CHADDR`)** field in the request (so server thinks each request is a different device).
3. DHCP server responds with `DHCPOFFER` and eventually leases all available IPs.
4. Server’s pool becomes **starved** (exhausted).


---
# Usage
```sh
dhcpstarv -i eth0
```