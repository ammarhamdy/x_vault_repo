

[How to install](https://github.com/bee-san/RustScan/wiki/Installation-Guide) 

https://github.com/bee-san/RustScan/releases

---

`RustScan` is a high-speed, open-source port scanner, often used with Nmap, that rapidly discovers open ports on a network using optimized algorithms and an adaptive learning engine. 

Developed in the Rust programming language, it automates the discovery of open ports and pipes the results to other tools for further analysis

----

# Greppable

When you run `RustScan`, you may notice that the initial output contains banners, author credits, and additional information not directly related to the scan results.

Use the -g (greppable) option to show only the scanning
information.

```sh
rustscan -g -a 192.168.1.0/24 -r 1-1024
```

# Scan a single IP
```sh
rustscan -a 192.168.1.10
```
`-a` = target IP or hostname

# Scan a range of IPs
```sh
rustscan -a 192.168.1.1-20
```

# Scan multiple IPs from a file
```sh
rustscan -a targets.txt
```

# Run Nmap automatically 
`RustScan` finds open ports, then hands them to Nmap:
```sh
rustscan -a 192.168.1.1 -- -sV -sC
```
`--` means: pass everything after this directly to Nmap

# Useful Flags

`-b <number>` → Batch size (how many ports to scan at once).
```sh
rustscan -a 192.168.1.1 -b 2000
```

`-t <ms>` → Timeout in milliseconds.
```sh
rustscan -a 192.168.1.1 -t 2000
```

`-p <ports>` → Specific ports (instead of config).
```sh
rustscan -a 192.168.1.1 -p 22,80,443
```

# Limited sockets on Linux 

`RustScan` needs a lot of file descriptors (sockets) open at once to scan ports fast.

By default, Linux/Mac limits this (often 1024), so `RustScan` warns you:
```sh
Your file limit is very small, which negatively impacts RustScan's speed.
Use the Docker image, or up the Ulimit with '--ulimit 5000'.
```

## Temporary Fix

Run this to increases the open files limit to 5000 for your current shell.
```sh
ulimit -n 5000
```

You can see current value with:
```sh
ulimit -n
```




