

`netdiscover` is a powerful ARP network scanner used to discover devices connected to a local network (LAN).

`netdiscover` table's headers:  
+ `IP`           
+ `At MAC Address`     
+ `Count`     
+ `Len` 
+ `MAC Vendor / Hostname` 

```shell
sudo netdiscover -r 192.168.1.0/24
```

----
# IP
The **IP address** of the device found on the local network
It’s the **Layer 3 (Network layer)** address assigned to the device.


# Count
**COUNT** means _how many ARP packets netdiscover has received_ from that host.
- More ARP packets ⇒ host is active and chatty on the network
- Very low count ⇒ the host responded only because Netdiscover probed it
- Extremely high count ⇒ usually routers, DHCP servers, gateways

Examples:
- A router may show a COUNT of 100+
- A phone or PC might show 5–20
- A quiet device with 1–2 was probably discovered by active ARP request only


# LEN
**LEN** means _total number of bytes of ARP traffic received_ from that host.
- Higher LEN ⇒ more traffic or larger ARP packets
- Usually correlates with COUNT
- Not very useful for security, but useful to see which devices are “noisy”

Example:
- COUNT = 10, LEN = 600 ⇒ average 60 bytes per ARP
- COUNT = 50, LEN = 3000 ⇒ host is very active on ARP network