

DHCP is an application-layer protocol responsible for allowing a device to automatically obtain an IP address.


# DHCP Packet Structure

**OpCode** 
	Indicates whether the packet is a DHCP request or a DHCP reply 

**Hardware Type** 
	The type of hardware address (`10MB` Ethernet, IEEE 802, ATM, and so on) 
	
**Hardware Length** 
	The length of the hardware address 

**Hops** 
	Used by relay agents to [assist](https://translate.google.com/?sl=en&tl=ar&text=assist&op=translate) in finding a DHCP server 

**Transaction ID**
	A random number used to pair requests with responses 
	
**Seconds Elapsed** 
	Seconds since the client first requested an address from the DHCP server 
	
**Flags** 
	The types of traffic the DHCP client can accept (unicast, broadcast, and so on)

**Client IP Address** 
	The client’s IP address (derived from the Your IP Address field) 

**Your IP Address** 
	The IP address offered by the DHCP server (ultimately becomes the Client IP Address field value) 

**Server IP Address** 
	The DHCP server’s IP address Gateway 
	
**IP Address** 
	The IP address of the network’s default gateway 

**Client Hardware Address** 
	The client’s MAC address 

**Server Host Name** 
	The server’s host name (optional) 

**Boot File** 
	A boot file for use by DHCP (optional) 

**Options**
	Used to expand the structure of the DHCP packet to give it more features


![[Pasted image 20250129163620.png]]


# The DHCP Initialization Process
The primary goal of DHCP is to assign addresses to clients during the initialization process.

The renewal process takes place between a single client and a DHCP server, as shown in the file `dhcp_nolease_initialization.pcapng`.

The DHCP initialization process is often referred to as the DORA process because it uses four types of DHCP packets: **==discover==**, **==offer==**, **==request==**, and **==acknowledgment==**

![[Pasted image 20250129164530.png]]

## The Discover Packet

![[Pasted image 20250204072741.png]]
As you can see in the referenced capture file, the first packet is sent from `0.0.0.0` on port `68` to `255.255.255.255` on port `67`. 

The client uses `0.0.0.0` because it does not yet have an IP address. 

The packet is sent to `255.255.255.255` because this is the network-independent broadcast address, thus ensuring that this packet will be sent out to every device on the network.

Because the device doesn’t know the address of a DHCP server, this first packet is sent in an attempt to find a DHCP server that will listen.

Examining the Packet Details pane, the first thing we notice is that ==**DHCP relies on UDP**== as its transport layer protocol.

The meat of this packet is in its four Option fields:
![[Pasted image 20250204073500.png]]

**DHCP Message Type** 
	This is option type `53`, with length `1` and a value of Discover (1). 
	These values indicate that this is a DHCP discover packet. 

**Client Identifier** 
	This provides additional information about the client requesting an IP address. 

**Requested IP Address** 
	This supplies the IP address the client would like to receive. 
	This can be a ==**previously used IP address**== or `0.0.0.0` to indicate no preference. 

**Parameter Request List** 
	This lists the different configuration items (IP addresses of other important network devices and other non IP items) the client would like to receive from the DHCP server.


## The Offer Packet
![[Pasted image 20250204074011.png]]
The second packet in this file lists valid IP addresses in its IP header, showing a packet traveling from `192.168.1.5` to `192.168.1.10`

The client ==**doesn’t actually have the**== `192.168.1.10` **==address yet==**, so the server will first attempt to communicate with the client using its hardware address, as provided by ARP.

If communication isn’t possible, the server will simply broadcast the offer to communicate.

The DHCP portion of this second packet, called the offer packet, indicates that the Message type is a reply. 

This packet contains the same ==**Transaction ID**== as the previous packet, which tells us that this reply is indeed a response to our original request.

![[Pasted image 20250204074440.png]]

![[Pasted image 20250204074429.png]]


## The Request Packet

Once the client receives an offer from the DHCP server, it should accept it with a DHCP request packet.

The third packet in this capture still comes from IP address `0.0.0.0`, because we have not yet completed the process of obtaining an IP address.

the Transaction ID field is the same as in the first two packets.

This packet is similar to the discover packet, in that all of its IP-addressing information is zeroed.

Finally, in the Option fields, we see that this is a DHCP Request Notice that the ==requested IP address is no longer blank== and that the DHCP Server Identifier field also contains an address.

![[Pasted image 20250204082223.png]]


## The Acknowledgment Packet
In the final step in this process, the DHCP server sends the requested IP addresses to the client in an acknowledgment packet and ==records that information in its database==.


## DHCP In-Lease Renewal (في تجديد الإيجار)
When a DHCP server assigns an IP address to a device, it [leases](https://translate.google.com/?sl=en&tl=ar&text=leases&op=translate) it to the client (يؤجرها للعميل).

This means that the client is allowed to use the IP address for only a limited amount of time before it must renew the lease.

The DORA process just discussed occurs the first time a client gets an IP address or when its lease time has expired.
In either case, the device is considered to be **==out of lease==**.

When a client with an IP address in-lease reboots, it must perform a truncated version of the DORA process in order to reclaim its IP address. 
This process is called an **==in-lease renewal==**.
In the case of a lease renewal, the discovery and offer packets are unnecessary.

You’ll find a sample capture of an in-lease renewal in the file `dhcp_inlease_renewal.pcapng`.


## DHCP Options and Message Types
`DHCP`’s real flexibility lies in its available options. As you’ve seen, the packet’s DHCP options can vary in size and content. 

The packet’s over all size depends on the combination of options used. 

You can view a full list of the many DHCP options at http://www.iana.org/assignments/bootp-dhcp-parameters/

==The only option **required** in all DHCP packets is the Message type option (option 53)==.

This option identifies how the DHCP client or server will process the information contained within the packet.
There are 8 message types:

| Number | Message Type | Description                                                                                                        |
| ------ | ------------ | ------------------------------------------------------------------------------------------------------------------ |
| 1      | Discover     | Used by the ==client== to locate available DHCP servers                                                            |
| 2      | Offer        | Sent by the ==server== to the client in response to a discover packet                                              |
| 3      | Request      | Sent by the ==client== to request the offered parameters from the server                                           |
| 4      | Decline      | Sent by the ==client== to the server to indicate invalid parameters within a packet                                |
| 5      | ACK          | Sent by the ==server== to the client with the configuration parameters requested                                   |
| 6      | NAK          | Sent by the ==client== to the server to refuse a request for configuration parameters                              |
| 7      | Release      | Sent by the ==client== to the server to cancel a lease by releasing its configuration parameters                   |
| 8      | Inform       | Sent by the ==client== to the server to ask for configuration parameters when the client already has an IP address |




# DHCP Version 6 (DHCPv6)
DHCPv6 was devised in `RFC3315`. 

Since DHCPv6 isn’t built on the concept of BOOTP, its packet format is much simpler.

![[Pasted image 20250205071842.png]]

The packet structure shown here contains only two static values, which function in the same manner as their DHCP counterparts. 

The rest of the packet structure varies depending on the message type identified in the first byte. 

Within the Options section, each option is identified with a 2-byte option code and a 2-byte length field. 

A full list of message types and option codes that can appear in these fields can be found here: http://www.iana.org/assignments/dhcpv6-parameters/dhcpv6-parameters.xhtml.

DHCPv6 accomplishes the same goal as DHCP, but to understand the flow of DHCPv6 communication, we must replace our DORA acronym with a new one, SARR.
![[Pasted image 20250205072109.png]]
Solicit (طلب, التمس), Advertise (أعلن).

**Solicit:** 
	An initial packet is sent from a client to a special multicast address (`ff02::1:2`) to attempt to locate available DHCPv6 servers on the network. 

**Advertise:** 
	An available server responds directly to the client to indicate that it is available to provide addressing and configuration information.

**Request:** 
	The client sends a formal request for configuration information to the server via multicast.
	
**Reply:** 
	The server sends all available requested configuration information directly to the client, and the process is complete.

See `dhcp6_outlease_acquisition.pcapng`.
This communication takes place over ports `546` and `547`, which are the standard ports used by DHCPv6.


