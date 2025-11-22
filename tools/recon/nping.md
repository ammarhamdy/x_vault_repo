
# Useful Options

| Option                     | Description                       |
| -------------------------- | --------------------------------- |
| `--rate <n>`               | Packets per second (default is 2) |
| `-c <n>`                   | Total number of packets           |
| `--data-length <n>`        | Payload size in bytes             |
| `--tcp`, `--udp`, `--icmp` | Protocol type                     |
| `--source-port <n>`        | Use specific source port<br>      |

# Basic Flooding with `nping`

**TCP Flood**
```bash
nping --tcp -p 80 --rate 1000 -c 100000 target-ip
```
- `--tcp`: Use TCP packets.
- `-p 80`: Target port 80 (change as needed).
- `--rate 1000`: Send 1000 packets per second.
- `-c 100000`: Total number of packets to send.
- `target-ip`: Replace with the actual IP of the target.

**UDP Flood Example**
```bash
nping --udp -p 53 --rate 5000 -c 100000 target-ip
```
- Uses UDP packets (port 53 is DNS — change to suit your test).
- UDP is faster and less resource-intensive to flood with.

**ICMP (Ping) Flood**
```bash
nping --icmp --rate 1000 -c 50000 target-ip
```
Sends raw ICMP Echo Requests (like `ping`, but at a high rate).


----
# `hping3` vs `nping`

| Feature             | `hping3`                            | `nping` (part of Nmap)                     |
| ------------------- | ----------------------------------- | ------------------------------------------ |
| Developed by        | Salvatore Sanfilippo (Antirez)      | Nmap Project                               |
| Part of             | Standalone tool                     | Included with Nmap                         |
| Protocol Support    | TCP, UDP, ICMP, RAW-IP              | TCP, UDP, ICMP, ARP                        |
| Scriptable Output   | No (awk/grep only)                  | Yes (can output JSON/XML-like formats)     |
| Easy Timing Control | Limited                             | Very fine control with `--rate`, `--delay` |
| NAT Detection       | No                                  | Yes (`--tr` mode)                          |
| Output Readability  | Raw, low-level                      | Clean, structured                          |
| Suitability         | Firewall testing, advanced crafting | Latency testing, packet tracing, scripting |
| Flooding Support    | Yes (`--flood`)                     | Not designed for flooding                  |
