
Run `man pcap-filter` for a complete guide.

BPF (Berkeley Packet Filter) syntax is used to filter network traffic efficiently. 
It’s commonly employed in tools like **`tcpdump`**, **`Wireshark`**, and **`libpcap`**. 
The syntax is designed to be concise and powerful, allowing users to specify packet filtering rules based on various fields.

Here's an overview of BPF syntax:

## Basic Structure

The general form of a BPF filter expression is:
```
[protocol] [direction] [type] [value]
```

**`protocol`**: Specifies the protocol (e.g., `ip`, `tcp`, `udp`, `arp`, `icmp`, etc.).

**`direction`**: Indicates the direction of traffic:
- `src`: Source address/port.
- `dst`: Destination address/port.
- `src or dst`: Either source or destination.
- `src and dst`: Both source and destination.

**`type`**: Identifies the type of value to match:
- `host`: An IP address or hostname.
- `port`: A port number.
- `net`: A network (with CIDR notation).

**`value`**: The specific value to match (e.g., an IP address, port number, or network).


## Examples

```
host 192.168.1.1
tcp dst port 80
udp src net 192.168.0.0/16
icmp
host 10.0.0.1
tcpdump -i eth0 tcp port 443
```

Filter based on packet size:
```
less 128
```

Filter multicast traffic:
```
ether multicast
```

Match specific bytes in the packet:
```
tcp[13] == 0x02
```

