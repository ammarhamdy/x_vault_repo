
The User Datagram Protocol (UDP) is the other layer 4 protocol commonly used on modern networks. 

While TCP is designed for reliable data delivery with built-in error checking, UDP aims to provide speedy transmission. 

For this reason, UDP is a best-effort service, commonly referred to as a connectionless protocol. 

A connectionless protocol doesn’t formally establish and terminate a connection between hosts, unlike TCP with its handshake and teardown processes.

The UDP header is much smaller and simpler than the TCP header.

==**The protocols that rely on UDP typically have their own built-in reliability services**== or use certain features of ICMP to make the connection somewhat more reliable.

**For example**, the application-layer protocols **DNS** and **DHCP**, which are highly dependent on the speed of packet transmission across a network, use UDP as their transport layer protocol, but they handle error checking and retransmission timers themselves.


# UDP Packet Structure

![[Pasted image 20250129155414.png]]

The UDP header is much smaller and simpler than the TCP header.

**Source Port** 
	The port used to transmit the packet 

**Destination Port** 
	The port to which the packet will be transmitted 

**Packet Length** 
	The length of the packet in bytes Checksum Used to ensure that the contents of the UDP header and data are intact upon arrival

The file `udp_dnsrequest.pcapng` contains one packet.

![[Pasted image 20250129155114.png]]


Any application that uses UDP must take special steps to ensure reliable delivery, if it is necessary. 

This is in contrast to TCP, which utilizes a formal connection setup and teardown, and has features in place to validate that packets were transmitted successfully.


