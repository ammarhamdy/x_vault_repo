

## Network Protocol Suites (الأجنحة):
+ Protocols must be able to work with other protocols.
+ Protocol suites are designed to work with each other seamlessly (بسلاسة).
+ ==**A protocol suite is**== ___a group of inter-related protocols necessary to perform a communication function.___


## Evolution of Protocol Suites:
+ A protocol suite is a set of protocols that work together to provide comprehensive network communication services.
+ Since the 1970s there have been several different protocol suites, some developed by a standards organization and others developed by various vendors.
+ There were several competing protocol suites:
	+ **Internet protocol suite (TCP/IP)**.
	+ **Open system interconnection (الترابط) (OSI) protocols**.
	+ **Apple Talk**.
	+ **Novell Netware**.
+ ![[Pasted image 20230212140949.png]]


## Internet protocol suite:
+ This is most common and relevant (مناسب) protocol suite used today.
+ Is an open standard protocol suite.
	+ This means it is freely available to the public and can be used by any vendor (بائع).
+ Maintained by the Internet Engineering Task Force (IETF).


## TCP/IP Protocol Example:
+ TCP/IP protocols are available for the application, transport, and internet layers. 
+ There are no TCP/IP protocols in the network access layer.
+ The most common network access layer LAN protocols are Ethernet and WLAN (wireless LAN) protocols.
+ Network access layer protocols are responsible for delivering the IP packet over the physical medium.


## TCP/IP Protocol Suite:
+ Today, the TCP/IP protocol suite includes many protocols and continues to evolve to support new services.
+ ![[Pasted image 20230212143747.png]]



---
## Application Layer:
+ DNS.
+ Host Config:
	+ DHCPv4
	+ DHCPv6
	+ SLAAC.
+ Email:
	+ SMTP
	+ POP3
	+ IMAP.
+ File transfer:
	+ FTP
	+ SFTP
	+ TFTP.
+ Web and web service:
	+ HTTP
	+ HTTPS
	+ REST.


### Name system (DNS):
+ **DNS** (Domain Name System). 
+ Translates domain names such as cisco.com, into IP addresses.


### Host Config (DHCPv4, DHCPv6, SLAAC):
+ **DHCPv4**:
	+ Dynamic Host Configuration Protocol for IPv4.
	+ A DHCPv4 server dynamically assigns IPv4 addressing information to DHCPv4 clients at start-up and allows the addresses to be re-used when no longer needed.
+ **DHCPv6**:
	+ Dynamic Host Configuration Protocol for IPv6.
	+ DHCPv6 is similar to DHCPv4 but for IPV6.
+ **SLAAC**:
	+ Stateless Address Autoconfiguration.
	+ A method that allows a device to obtain its IPv6 addressing information without using a DHCPv6 server.


### Email (SMTP, POP3, IMAP):
+ **SMTP**:
	+ Simple Mail Transfer Protocol.
	+ Enables clients to send email to a mail server and enables servers to send email to other servers.
+ **POP3**:
	+ Post Office Protocol version 3.
	+ Enables clients to retrieve email from a mail server and download the email to the client's local mail application.
+ **IMAP**:
	+ Internet Message Access Protocol.
	+ Enables clients to access email stored on a mail server as well as maintaining email on the server.


### File transfer (FTP, SFTP, TFTP):
+ **FTP**:
	+ File Transfer Protocol.
	+ Sets the rules that enable a user on one host to access and transfer files to and from another host over a network.
	+ FTP is a reliable, connection-oriented, and acknowledged file delivery protocol.
+ **SFTP**:
	+ SSH File Transfer Protocol.
	+ As an extension to Secure Shell (SSH) protocol, SFTP can be used to establish a secure file transfer session in which the file transfer is encrypted.
	+ SSH is a method for secure remote login that is typically used for accessing the command line of a device.
+ **TFTP**:
	+ Trivial File Transfer Protocol.
	+ A simple, connectionless file transfer protocol with best-effort, unacknowledged file delivery.
	+ It uses less overhead than FTP.


### Web and web service (HTTP, HTTPS, REST):
+ **HTTP**:
	+ Hypertext Transfer Protocol.
	+ A set of rules for exchanging text, graphic images, sound, video, and other multimedia files on the World Wide Web.
+ **HTTPS**:
	+ HTTP Secure.
	+ A secure form of HTTP that encrypts the data that is exchanged over the World Wide Web.
+ **REST**:
	+ Representational State Transfer.
	+ A web service that uses application programming interfaces (APIs) and HTTP requests to create web applications.



---
## Transport layer:
+ TCP.
+ UDP.


### Connection-Oriented, TCP:
+ Transmission Control Protocol.
+ Enables reliable communication between processes running on separate hosts and provides reliable, acknowledged transmissions that confirm successful delivery.


### Connectionless, UDP:
+ User Datagram Protocol.
+ Enables a process running on one host to send packets to a process running on another host.
+ UDP does not confirm successful datagram transmission.



---
## Internet Layer:
+ Internet Protocols:
	+ IPv4.
	+ IPv6.
	+ NAT.
+ Messaging Protocols:
	+ ICMPv4. 
	+ ICMPv6. 
	+ ICMPv6 ND.
+ Routing Protocols:
	+ OSPF.
	+ EIGRP.
	+ BGP.


### Internet Protocols (IPv4, IPv6):
+ **IPv4**:
	+ Internet Protocol version 4.
	+ Receives message segments from the transport layer.
	+ Packages messages into packets.
	+ Addresses packets for end-to-end delivery over a network.
	+ IPv4 uses a 32-bit address.
+ **IPv6**:
	+ IP version 6.
	+ Similar to IPv4 but uses a 128-bit address.
+ **NAT**:
	+ Network Address Translation.
	+ ==Translates IPv4 addresses from a private network into globally unique public IPv4 addresses.==


### Messaging Protocols (ICMPv4, ICMPv6, ICMPv6 ND):
+ **ICMPv4**:
	+ Internet Control Message Protocol for IPv4.
	+ Provides feedback from a destination host to a source host about errors in packet delivery.
+ **ICMPv6**:
	+  ICMP for IPv6.
	+ Similar functionality to ICMPv4 but is used for IPv6 packets.
+ **ICMPv6 ND**: 
	+ ICMPv6 Neighbor Discovery.
	+ Includes four protocol messages that are used for address resolution and duplicate address detection.


### Routing Protocols (OSPF, EIGRP, BGP):
+ **OSPF**:
	+ Open Shortest Path First.
	+ Link-state routing protocol that uses a hierarchical design based on areas.
	+ OSPF is an open standard interior routing protocol.
+ **EIGRP**:
	+ Enhanced Interior Gateway Routing Protocol.
	+ An open standard routing protocol developed by Cisco that uses a composite metric based on bandwidth, delay, load and reliability.
+ **BGP**:
	+ Border Gateway Protocol.
	+ An open standard exterior gateway routing protocol used between Internet Service Providers (ISPs).
	+ BGP is also commonly used between ISPs and their large private clients to exchange routing information.



---
## Network Access Layer:
+ ARP.
+ Data Link Protocols:
	+ Ethernet. 
	+ WLAN.


### Address Resolution (ARP):
+ Address Resolution (دقة) Protocol.
+ Provides dynamic address mapping between an IPv4 address and a hardware address.


### Data Link Protocols (Ethernet, WLAN):
+ **Ethernet**:
	+ Defines the rules for wiring and signaling standards of the network access layer.
+ **WLAN**:
	+ Wireless Local Area Network.
	+ ==Defines the rules for wireless signaling across the 2.4 GHz and 5 GHz radio frequencies.==


---
## TCP/IP Communication Process:
+ ![[TCP-IP-Communication-Process.gif]]
+ ![[Pasted image 20230212173846.png]]
