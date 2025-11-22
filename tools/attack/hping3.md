
https://www.kali.org/tools/hping3/

[[nping#`hping3` vs `nping`]]


`hping3` is a powerful **network packet crafting** and **analysis tool**, similar to `ping`, but with far more control. 

You can use it to send **custom TCP/IP packets**, perform **port scanning**, **DoS testing**, **firewall testing**, and **network diagnostics**.

```bash
sudo apt install hping3
```

---

# Common Use Cases & Examples


## 1. **Ping with TCP instead of ICMP**
```bash
hping3 -S -p 80 google.com
```
* `-S`: Sends TCP SYN packets (like a SYN scan)
* `-p 80`: Target port 80 (HTTP)
* Good for checking if a port is open when ICMP is blocked (e.g., by firewalls)

## 2. **ICMP Ping (like normal ping)**
```bash
hping3 --icmp google.com
```
* Sends ICMP Echo Request packets (standard ping)

## 3. **SYN Scan (like Nmap stealth scan)**
```bash
hping3 -S -p 1-100 192.168.1.1
```
* Sends SYN packets to ports 1 through 100
* Useful to discover open TCP ports

## 4. **TCP Connect Scan (3-way handshake)**
```bash
hping3 -S -p 22 --tcp-timestamp 192.168.1.1
```
* Use this only on systems you own or have permission to scan

## 5. **Flood Attack (DoS Simulation)**
```bash
sudo hping3 -S --flood -p 80 192.168.1.100
```
* `--flood`: Sends packets as fast as possible

