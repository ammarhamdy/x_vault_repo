
# The `ifconfig` Command (deprecated)


## Interface configuration:
+ The `ifconfig` command stands for interface configuration and is used to display network configuration information.
+ it is important to note from the output below that the IP address of the primary network device `eth0` is `192.168.1.2` and that the device is currently active `UP`
![[Pasted image 20240227040821.png]]
+ The `lo` device is referred to as the loopback device. It is a special network device used by the system when sending network-based data to itself.
+ The `ifconfig` command can also be used to modify network settings temporarily (مؤقتا).



---
# The route Command (deprecated)


## What can `route` do:
+ Recall that a router (or gateway) is a machine that allows hosts from one network to communicate with another network.
+ To view a table that describes where network packages are sent, use the `route` command:
![[Pasted image 20240227041805.png]]
+ The first highlighted line in the preceding example indicates that any network packet sent to a machine in the `192.168.0`
+ The second highlighted line indicates that all other network packets are sent to the host with the IP address of `192.168.1.1` (the router).
+ Some users prefer to display this information with numeric data only, by using the `-n` option to the `route` command.
![[Pasted image 20240227041927.png]]
+ The `0.0.0.0` refers to all other machines, and is the same as default.
+ The `route` command is becoming obsolete in some Linux distributions (deprecated) and is being replaced with a form of the `ip` command, specifically `ip route` or `ip route show`.
+ Note that the same information highlighted above can also be found using this command
```
ip route show
```



----
# The netstat Command (deprecated)


The `netstat` command is a powerful tool that provides a large amount of network information. 
It can be used to display information about network connections as well as display the routing table similar to the `route` command.


## Network statistics:
+ For example, to display statistics regarding network traffic, use the `-i` option to the `netstat` command:
```
root@localhost:~# netstat -i  
```


## Show routing information:
+ To use the `netstat` command to display routing information, use the `-r` option:
```
root@localhost:~# netstat -r
```


## Port number:
+ The `netstat` command is also commonly used to display open ports.
+ ==A port is a unique number that is associated with a service provided by a host. ==
+ ==If the port is open, then the service is available for other hosts.==
+ For example, you can log into a host from another host using a service called SSH. 
+ The SSH service is assigned port #22. 
+ So, if port #22 is open, then the service is available to other hosts.
+ To see a list of all currently open ports, use the following command:
```
root@localhost:~# netstat -tln  
```
+ In the previous example, `-t` stands for TCP.
+ `-l` stands for listening (which ports are listening) and `-n` stands for show numbers, not names.


## `netstat` is obsolete:
+ On some distributions you may see the following message in the man page of the `netstat` command:
```
NOTE
     This program is obsolete. 
     Replacement for netstat is ss. 
     Replacement for netstat -r is ip route.
     Replacement for netstat -i is ip -s link. 
     Replacement for netstat -g is ip maddr.
```
+ The goal is to eventually replace the `netstat` command with commands such as the `ss` and `ip` commands.




----
# The `ARP` command (deprecated)

[arp](obsidian://open?vault=x_vault&file=networking%2FCCNA%20V_7%2FIntroduction%20to%20Networks%2F8.%20Address%20Resolution%2F2.%20ARP) 

**To show the current ARP table:**
```sh
arp -a
```

**To manually add a permanent ARP entry:**
```sh
sudo arp -s <IP_ADDRESS> <MAC_ADDRESS>
```

**To remove an ARP entry:**
```sh
sudo arp -d <IP_ADDRESS>
```


The `arp` command is now deprecated on many modern Linux systems, and the **`ip`** command (from the `iproute2` package) is used instead. 

Equivalent tasks with `ip`:

**View ARP Table:**
```sh
ip neighbor show
```

**Add a Static ARP Entry:**
```sh
sudo ip neighbor add <IP_ADDRESS> lladdr <MAC_ADDRESS> dev <INTERFACE>
```

**Delete an ARP Entry:**
```sh
sudo ip neighbor del <IP_ADDRESS> dev <INTERFACE>
```

**Clear the ARP cache if there are connectivity issues:**
```sh
sudo ip neigh flush all
```

