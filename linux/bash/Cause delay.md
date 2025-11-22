
# Basic Delays
Pauses for a Specified Time
```sh
sleep 10  # Delays for 10 seconds
```
Using Read to Wait for Input
```sh
read -p "Press Enter to continue..."
```


# CPU-Intensive Delays
Fork Bomb (Dangerous – Crashes System! ⚠️)
This creates an infinite loop of processes that consume system resources.
```sh
:(){ :|:& };:
```
To recover: **Reboot or switch to another TTY (`Ctrl + Alt + F3`) and kill the processes.**


# Disk and I/O Delays
Create a Large Dummy File
```sh
dd if=/dev/zero of=bigfile bs=1M count=10000  # Creates a 10GB file
```
Slow Disk Read
```sh
cat /dev/urandom > /dev/null  # Reads random data endlessly
```
Slow Find Command
```sh
find / -type f > /dev/null  # Searches all files in the system
```


# Network-Related Delays
Ping a Nonexistent IP (Timeout)
```sh
ping -w 30 192.0.2.123  # Pings an unreachable IP for 30 seconds
```
Limit Network Speed
```sh
sudo tc qdisc add dev eth0 root netem delay 500ms  # Adds 500ms delay to network
```
To remove the delay:
```sh
sudo tc qdisc del dev eth0 root
```

