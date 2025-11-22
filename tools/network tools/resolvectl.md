
This command is used on **Linux systems** (especially those using **systemd**, like Ubuntu, Debian, Fedora, etc.) to **check your system's DNS (Domain Name System) configuration**.

It's part of the `systemd-resolved` service, which handles DNS name resolution for your system.

```sh
resolvectl status
```
- Shows the **default DNS servers** your system is using.
- Includes **fallback servers** (in case the main ones fail).
- May list **DNSSEC** status (a security feature for DNS).


**Link-specific DNS Settings**
For each network interface (like `eth0`, `wlan0`, etc.), you'll see:
- **Current DNS servers** being used for that interface.
- The **search domains** (used when you try to resolve short host-names).
- Whether DNS is enabled for that link.
- The **protocols in use** (e.g. `DNS`, `LLMNR`, `MulticastDNS`, `DNSOverTLS`).
- Whether the system is using a VPN or custom DNS setup.


