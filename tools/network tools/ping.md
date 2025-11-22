

The `ping` command can be used to determine if another machine is reachable. 
If the `ping` command can send a network package to another machine and receive a response, then you should be able to connect to that machine.

## Send and receive limit amount:
By default, the `ping` command continues sending packages endlessly. 

To limit how many pings to send, use the `-c` option followed by a number indicating how many iterations you desire. 

The following examples show `ping` being limited to 4 iterations.
```
ping -c 4 192.168.1.2    
```


## Not useful in all times:
As a result, the `ping` command may be useful for checking the availability of local machines, but not always for machines outside of your own network.


## Use `ping` for:
Many administrators use the `ping` command with a hostname, and if that fails then use the IP address to see if the fault is in resolving the device’s hostname.

Using the hostname first saves time; if that `ping` command is successful, there is proper name resolution, and the IP address is functioning correctly as well.


**Ping a specific interface:**
```
ping -I <interface> <destination>
```

**Ping time out:**
```
ping -W <timeout_in_seconds> <target_host>
```

---
# TTL


The **TTL (Time To Live)** you see in `ping` results is not random — it depends on the **operating system** of the target device (and sometimes routers in between).

TTL is a number in the IP packet header that decrements by **1 at each hop** (router) the packet passes.
    
When TTL reaches `0`, the packet is discarded to avoid infinite loops.

# Why 64 vs 128?

Different operating systems use **different default starting TTL values**:

| Default TTL | Common Systems                  |
| ----------- | ------------------------------- |
| **64**      | Linux, macOS, Android, Unix     |
| **128**     | Windows (all versions)          |
| **255**     | Some Cisco routers, BSD systems |

So:
- If you ping a **Windows machine**, you’ll usually see `ttl=128`.
- If you ping a **Linux server** or a router, you’ll often see `ttl=64`.
- The actual number you see is `default - hops`.

Example:
- Windows host (default 128), 2 hops away → `ttl=126`.
- Linux host (default 64), same distance → `ttl=62`.

