

Perfect — Scapy is a **powerful Python-based network tool** that can **craft, send, sniff, and analyze packets**. 

You can use it both from the **terminal (interactive shell)** and as a **Python library**. 

Let’s go step by step so you learn both sides properly.


---
# What Scapy Is

**Scapy** is a packet manipulation tool that lets you:

- Create and send custom packets (e.g. IP, TCP, UDP, ARP, ICMP)

- Sniff network traffic

- Perform `traceroutes`

- Scan networks and ports

- Create network attacks (for learning or simulation purposes — ethically!)

---
# Basics

## Run the interactive shell
```
sudo scapy
```

## list all Scapy commands
```
lsc()
```

## list fields of IP layer
```
ls(IP)
```


---
# L2–L7 / TCP-IP stack

Scapy actually manipulates (L2–L7 / TCP-IP stack)

![[5. Reference Models#Layers and it's protocols]]