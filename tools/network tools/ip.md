

The `ifconfig` command is becoming obsolete in some Linux distributions (deprecated) and is being replaced with a form of the `ip` command, specifically `ip addr show`.

The `ip` command differs from `ifconfig` in several important manners, chiefly (على رأسها) that through its increased functionality and set of options, it can almost be a one-stop shop for configuration and control of a system’s networking. 

The format for the `ip` command is as follows:
```
ip [OPTIONS] OBJECT {COMMAND} [ARGUMENTS]
```
**`OBJECT`**: Specifies the type of networking object (e.g., `link`, `address`, `route`).
**`COMMAND`**: The action to perform (e.g., `add`, `show`, `delete`).


##  Displaying Network Information:

**Show all network interfaces:**
```
ip link show
```

**Show IP addresses and related information:**
```
ip address show
```

**Show only active interfaces:**
```
ip -brief address
```
for more details:
```
ip link show
```


## Managing Network Interfaces

`sudo ip link set dev <interface> up | down`

**Bring an interface up:**
```
sudo ip link set dev wlo1 up
```

**Bring an interface down:**
```
sudo ip link set dev wlo1 down
```


## Configuring IP Addresses

**Assign an IP address to an interface:**
`sudo ip address add <IP>/<PREFIX> dev <interface>`
```
sudo ip address add 192.168.1.100/24 dev wlo1
```

**Remove an IP address:**
```
sudo ip address del <IP>/<PREFIX> dev <interface>
```


## Managing Routes

**Show the routing table:**
```
ip route show
```

**Add a route:**
`sudo ip route add <destination> via <gateway> dev <interface>`
```
sudo ip route add 10.0.0.0/24 via 192.168.1.1 dev wlo1
```

**Delete a route:**
```
sudo ip route del <destination>
```

**Delete the Default Gateway**
```
sudo ip route del default
```

**Add a Default Gateway**
```
sudo ip route add default via 192.168.1.1
```

## Managing ARP (Address Resolution Protocol)

**Show the ARP table:**
```
ip neighbor show
```

**Add a static ARP entry:**
```
sudo ip neighbor add <IP> lladdr <MAC_ADDRESS> dev <interface>
```

**Delete an ARP entry:**
```
sudo ip neighbor del <IP> dev <interface>
```


## Monitoring and Troubleshooting

**Monitor link and address changes:**
```
ip monitor all
```


## Default Gateway

**View the Default Gateway:**
```
ip route show default
```

**Set a Default Gateway:**
```
sudo ip route add default via 192.168.1.1 dev wlo1
```

