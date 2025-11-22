
The ultimate goal of the ==Transmission Control Protocol (TCP)== is to provide endto-end reliability for the delivery of data.

TCP, which is defined in **==RFC 793==**, handles data sequencing and error recovery, and ultimately ensures that data gets where it’s supposed to go. 

TCP is considered a connection-oriented protocol because it ==establishes a formal connection before transmitting data==, ==tracks packet delivery==, and usually ==attempts to formally close communication channels when transmission is complete==. 

Many commonly used application-layer protocols rely on TCP and IP to deliver packets to their final destination.


# TCP Packet Structure

![[Pasted image 20250129110205.png]]


**Source Port** 
	The port used to transmit the packet. 

**Destination Port** 
	The port to which the packet will be transmitted (the port that suppose to receive the packet). 

**Sequence Number**
	The number used to identify a TCP segment. 
	==This field is used to ensure that parts of a data stream are not missing.== 

**Acknowledgment Number** 
	The sequence number that is to be expected in the next packet from the other device taking part in the communication.

 **Flags** 
	 The `URG`, `ACK`, `PSH`, `RST`, `SYN`, and `FIN` flags for identifying the type of TCP packet being transmitted. 
	 
**Window Size** 
	The size of the TCP receiver buffer in bytes. 

**Checksum** 
	Used to ensure the contents of the TCP header and data are [intact](https://translate.google.com/?sl=en&tl=ar&text=intact&op=translate) upon arrival. 
	
**Urgent Pointer** 
	If the `URG` flag is set, this field is examined for additional instructions for where the CPU should begin reading the data within the packet.

 **Options** 
	 Various optional fields that can be specified in a TCP packet.


# TCP Ports

All TCP communication takes place using source and destination ports, which can be found in every TCP header. 

To transmit data to a particular application on a remote server or device, a TCP packet must know the port the remote service is listening on.

If you try to access an application on a port other than the one configured for use, the communication will fail.

**==The source port in this sequence isn’t incredibly important and can be selected randomly.==**
==The remote server will simply determine the port to communicate with from the original packet it’s sent.==

![[Pasted image 20250129110854.png]]


==There are **65,535** ports available for use when communicating with TCP.==
We typically divide these into two groups:

**The system port group (also known as the standard port or well-known port group)** 
==is from 1 through 1023== (ignoring 0 because it’s reserved). 
Well-known, established services generally use ports that lie within the system port grouping.

**The [ephemeral](https://translate.google.com/?sl=en&tl=ar&text=ephemeral&op=translate) port group** 
==Is from **1024** through **65535**== (although some operating systems have different definitions for this). 

==Only one service can communicate on a port at any given time, so modern operating systems select source ports randomly in an effort to make communications unique.== 

These source ports are typically located in the ephemeral range.

Let’s examine a couple of TCP packets and identify the port numbers they are using by opening the file `tcp_ports.pcapng`.

**Disable Transport Name Resolution**
Wireshark maintains a list of ports and their most common uses. 
Although system ports are primarily the ones with labeled common uses, many ephemeral ports have commonly used services associated with them. 
The labeling of these ports can be confusing, so it’s typically best to disable it by turning off transport name resolution. 
To do this, go to `Edit > Preferences > Name Resolution` and uncheck Enable Transport Name Resolution.


# The TCP Three-Way Handshake

All TCP-based communication must begin with a handshake between two hosts. 

This handshake process serves several purposes:

+ It allows the transmitting host to ensure that the recipient host is up and able to communicate.  

+ It lets the transmitting host check that the recipient is listening on the port the transmitting host is attempting to communicate on. 

+ It allows the transmitting host to send its starting sequence number to the recipient so that both hosts can keep the stream of packets in proper sequence.

The TCP handshake occurs in three steps:
![[Pasted image 20250129112849.png]]
==A handshake occurs before every TCP communication sequence.==

**In the first step** 
	The device that wants to communicate (host A) sends a TCP packet to its target (host B). 
	This initial packet contains no data other than the lower-layer protocol headers. 
	The TCP header in this packet has the `SYN` flag set and includes the initial sequence number and maximum segment size (`MSS`) that will be used for the communication process. 
![[Pasted image 20250129113639.png]]
**Then**
	Host B responds to this packet by sending a similar packet with the `SYN` and `ACK` flags set, along with its initial sequence number. 
![[Pasted image 20250129113752.png]]

**Finally** 
	Host A sends one last packet to host B with only the `ACK` flag set. 
	Once this process is completed, both devices should have all of the information they need to begin communicating properly.


**Acknowledgment number:**
**SECOND PACKET:**
![[Pasted image 20250129113940.png]]
`acknowledgment number (3691127925)`
The acknowledgment number shown here is 1 more than the ==**sequence** number== included in the ==**previous** packet== because ==this field is used to specify the **next** sequence number the host expects to receive==:
**FIRST PACKET:**
![[Pasted image 20250129114022.png]]

The final packet is the ACK
**FINAL PACKET:**
![[Pasted image 20250129114901.png]]
This packet, as expected, contains the ==**sequence** number== `3691127925` as defined in the previous packet’s Acknowledgment number field.



# TCP Teardown

The TCP teardown is used to gracefully end a connection between two devices after they have finished communicating.

This process involves four packets, and it utilizes the `FIN` flag to signify the end of a connection.

In a teardown sequence: 
**Host A** tells host B that it is finished communicating by sending a TCP packet with the FIN and ACK flags set.
**Host B** responds with an ACK packet and transmits its own FIN/ACK packet. 
**Host A** responds with an ACK packet, ending the communication.

![[Pasted image 20250129143723.png]]


To view this process in Wireshark, open the file `tcp_teardown.pcapng`.


# TCP Resets
In an ideal world, every connection would end gracefully with a TCP teardown. 

In reality, connections often end abruptly فجأة.  

For example, a host may be miss-configured, or a potential attacker may perform a port scan.

In these cases, ==when a packet is sent to a device that is not willing to accept it==, a TCP packet with the RST flag set may be sent. 

==**The RST flag is used to indicate that a connection was closed abruptly or to refuse a connection attempt.**==

The file `tcp_refuseconnection.pcapng` displays an example of network traffic that includes an RST packet.

![[Pasted image 20250129150642.png]]


The first packet in this file is from the host at `192.168.100.138`, which is attempting to communicate with `192.168.100.1` on port 80. 

What this host doesn’t know is that `192.168.100.1` isn’t listening on port 80 because it’s a Cisco router with no web interface configured. 

There is no service configured to accept connections on that port.
In response to this attempted communication, `192.168.100.1` sends a packet to `192.168.100.138` telling it that communication won’t be possible over port 80.

==**An RST packet ends communication whether it arrives at the beginning of an attempted communication sequence**==, as in this example, or is sent in the middle of the communication between hosts.


**RST** refers to the **Reset** flag (Like ACK, SYN, ..). 

It is one of the control flags in the TCP header that signals the termination of a connection or the rejection of a packet. 

The RST flag is used to indicate an error or an abnormal condition in the TCP communication.

### Key Characteristics of the RST Flag

1. **Immediate Termination**:
    - When a TCP segment with the RST flag set is sent, it immediately terminates the connection without going through the graceful **FIN** (finish) handshake.
        
2. **Connection Issues**:
    - Typically used when one side receives a packet that it cannot process or associate with an existing connection.
        
3. **No Acknowledgment**:
    - RST segments are not acknowledged, as they indicate an abnormal situation.

## When Is the RST Flag Used?

1. **Connection Refused**:
    - If a server receives a packet for a port where no application is listening, it responds with an RST to reject the connection.
        
2. **Invalid Packet**:
    - If a host receives a packet that doesn’t match an established connection (e.g., unexpected sequence numbers or closed socket).
        
3. **Abrupt Termination**:
    - A host can send an RST to terminate the connection abruptly (e.g., due to an error or application crash).
        
4. **Firewall or IDS Behavior**:
    - Firewalls or Intrusion Detection Systems may generate RST packets to block unwanted connections.


|Filter|Description|
|---|---|
|`!tcp.port==3389`|Filter out RDP traffic|
|`tcp.flags.syn==1`|TCP packets with the SYN flag set|
|`tcp.flags.reset==1`|TCP packets with the RST flag set|
|`!arp`|Clear ARP traffic|
|`http`|All HTTP traffic|
|`tcp.port==23||
|`smtp||