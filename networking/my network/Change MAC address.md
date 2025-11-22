

Changing your MAC address (**Media Access Control address**) on Ubuntu

# Impermanent Change

## **Check Your Current MAC Address:**
```
ip link show
```
or
```
sudo netplan status
```

## **Disable the Network Interface**
To safely change the MAC address, first disable the network interface:
```
sudo ip link set <interface> down
```
Replace `<interface>` with your network interface name, such as `eth0` or `wlan0`.

## **Change the MAC Address**
Set the new MAC address using the following command:
```
sudo ip link set <interface> address <new-mac-address>
```
Replace `<new-mac-address>` with the desired MAC address, e.g., `00:11:22:33:44:55`.

## **Enable the Network Interface**
Re-enable the network interface after setting the new MAC address:
```
sudo ip link set <interface> up
```

## **Verify the Change**
Confirm the new MAC address has been applied:
```
ip link show <interface>
```


# Make the Change Persistent 

To make the MAC address change persistent across reboots:

Edit the `Netplan` configuration file (e.g., `/etc/netplan/01-netcfg.yaml`):
```
sudo nano /etc/netplan/<file_name>
```

Add the `macaddress` property under the desired interface:
```
network: 
	version: 2 
	ethernets: 
		eth0: 
			dhcp4: true 
			macaddress: 00:11:22:33:44:55
```

Apply the configuration:
```
sudo netplan apply
```


---
## OUI lookup:
+ To find the ==**manufacturer**==, use the keywords IEEE OUI standards to find an OUI lookup tool on the internet or navigate to http://standards-oui.ieee.org/oui.txt to find the registered OUI vendor codes. 
+ The last six digits are the NIC serial number assigned by the manufacturer.


### **How to Use an OUI Lookup Tool**

**Online OUI Lookup Tools**
There are several online tools to perform OUI lookups:
- [IEEE OUI Lookup Tool](https://standards.ieee.org/products-services/regauth/oui/index.html)
- Wireshark OUI Lookup
- [MAC Vendors](https://macvendors.com/)


**Command-Line Tools**
You can also perform OUI lookups on your system:
Linux: Install arp-scan:
```
sudo apt install arp-scan
arp-scan --localnet
```

