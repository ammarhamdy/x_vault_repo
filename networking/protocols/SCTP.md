
**SCTP** stands for **Stream Control Transmission Protocol**. 

It's a transport-layer protocol (like TCP and UDP), defined by the IETF in [RFC 4960](https://datatracker.ietf.org/doc/html/rfc4960), designed to transmit multiple streams of data between two endpoints reliably and efficiently.


SCTP is:
- **Connection-oriented** like TCP (ensures data arrives in order)
- **Message-based** like UDP (preserves message boundaries)
- Supports **multi-streaming** and **multi-homing**, which TCP and UDP don’t offer

---
# Key Features

| Feature            | SCTP               | TCP   | UDP   |
| ------------------ | ------------------ | ----- | ----- |
| Reliability        | ✅ Yes              | ✅ Yes | ❌ No  |
| Ordering           | ✅ Yes (per stream) | ✅ Yes | ❌ No  |
| Message Boundaries | ✅ Yes              | ❌ No  | ✅ Yes |
| Multi-streaming    | ✅ Yes              | ❌ No  | ❌ No  |
| Multi-homing       | ✅ Yes              | ❌ No  | ❌ No  |
| Congestion Control | ✅ Yes              | ✅ Yes | ❌ No  |

- **Reliable, connection-oriented** transport like TCP.

- **Multi-streaming:** Multiple streams within one connection (association) prevent head-of-line blocking.

- **Multi-homing:** A host can have multiple IP addresses; SCTP can switch between them if one fails.

- **Message-oriented:** Like UDP, but reliable.

- **Four-way handshake** for association setup (more secure than TCP's three-way).

## Multi-Streaming
- SCTP can send multiple **independent data streams** in one connection (called an association).
- This avoids **head-of-line blocking** — when one blocked packet holds up all others (a TCP issue).

## Multi-Homing
- One SCTP endpoint can have **multiple IP addresses**.
- If one path fails, SCTP can switch to another without dropping the connection — **built-in fail-over**.

---
# Use Cases

**Telecom signaling** (original purpose — `SS7` over IP)

**`WebRTC`** data channels

**Diameter protocol** (used in `4G`/`LTE` infrastructure)

**Mission-critical systems** (where fail-over is important)

---
# Basic Working of SCTP

## Association Establishment (4-way Handshake)
```
Client                                Server
  | -------- INIT ------------------> |
  | <------- INIT ACK --------------- |
  | -------- COOKIE ECHO -----------> |
  | <------- COOKIE ACK ------------- |
```
- **INIT**: Client initiates association.
- **INIT ACK**: Server responds with parameters.
- **COOKIE ECHO**: Client sends back a "cookie" (security token).
- **COOKIE ACK**: Server acknowledges. Association is now established.

## Data Transfer with Streams
SCTP uses **streams** to separate data within a single association. 
For example:
```
SCTP Association
  ├── Stream 0: Voice packets
  ├── Stream 1: Video packets
  └── Stream 2: Control messages
```
Each stream has **its own sequence numbers**, avoiding head-of-line blocking. 
If a packet is lost in Stream 1, Stream 0 and 2 can still deliver their messages.

## Multi-Homing
Each endpoint can have multiple IP addresses:
```
Client (IP1, IP2) <==> Server (IP3, IP4)

If IP1 ↔ IP3 fails,
SCTP can reroute to IP2 ↔ IP4 without dropping the connection.

```

---
# Packet structure

![[Drawing 2025-07-02 11.22.29.excalidraw]]

## SCTP Packet Structure Overview
An SCTP packet is composed of:
1. A **common header**
2. One or more **chunks** (each chunk serves a specific function like control, data, etc.)
```diff
+--------------------------+
|       Common Header      |  ← Fixed size: 12 bytes
+--------------------------+
|         Chunk #1         |
+--------------------------+
|         Chunk #2         |
+--------------------------+
|           ...            |
+--------------------------+
|         Chunk #N         |
+--------------------------+
```

## Common Header (12 bytes):

| Field            | Size    | Description                                 |
| ---------------- | ------- | ------------------------------------------- |
| Source Port      | 2 bytes | Port number of sender                       |
| Destination Port | 2 bytes | Port number of receiver                     |
| Verification Tag | 4 bytes | Identifies association (like connection ID) |
| Checksum         | 4 bytes | Error-checking (uses CRC32c)                |
## Chunk Format (variable length)

Each chunk has its own format and purpose. 
Common chunk types include:
- INIT
- DATA
- SACK (Selective Acknowledgement)
- HEARTBEAT
- COOKIE ECHO/ACK
- SHUTDOWN

### SCTP Chunk Type Values

|Chunk Type Name|Hex Value|Decimal Value|Description|
|---|---|---|---|
|**DATA**|`0x00`|0|Carries user data|
|**INIT**|`0x01`|1|Initiates an association|
|**INIT ACK**|`0x02`|2|Responds to INIT|
|**SACK**|`0x03`|3|Acknowledges received DATA chunks|
|**HEARTBEAT**|`0x04`|4|Tests the reachability of a path|
|**HEARTBEAT ACK**|`0x05`|5|Acknowledges a HEARTBEAT chunk|
|**ABORT**|`0x06`|6|Aborts the association|
|**SHUTDOWN**|`0x07`|7|Graceful termination of an association|
|**SHUTDOWN ACK**|`0x08`|8|Acknowledges SHUTDOWN|
|**ERROR**|`0x09`|9|Reports error conditions|
|**COOKIE ECHO**|`0x0A`|10|Sends cookie back to the initiator|
|**COOKIE ACK**|`0x0B`|11|Final step to establish the association|
**Common Use in Practice:**
- **Association Setup**: `INIT`, `INIT ACK`, `COOKIE ECHO`, `COOKIE ACK`
- **Data Transfer**: `DATA`, `SACK`, `HEARTBEAT`, `HEARTBEAT ACK`
- **Connection Termination**: `SHUTDOWN`, `SHUTDOWN ACK`, `ABORT`

## Chunk Structure (General):

|Field|Size|Description|
|---|---|---|
|Type|1 byte|Chunk type (e.g., 0x00 for DATA)|
|Flags|1 byte|Depends on chunk type|
|Length|2 bytes|Total length of the chunk (including header)|
|Chunk-Specific|Variable|Data specific to the chunk type|

## DATA Chunk Structure

|Field|Size|Description|
|---|---|---|
|Type (0x00)|1 byte|Identifies this as a DATA chunk|
|Flags|1 byte|E.g., U (unordered), B (beginning), E (end)|
|Length|2 bytes|Length of the chunk|
|TSN (Transmission Sequence Number)|4 bytes|Used for ordering and reliability|
|Stream Identifier|2 bytes|Stream number (for multi-streaming)|
|Stream Sequence No|2 bytes|Message ordering within stream|
|Payload Protocol ID|4 bytes|Upper-layer protocol identifier|
|User Data (payload)|Variable|Actual user data|


## Text Diagram of an SCTP Packet (Example with One DATA Chunk):

```diff
+--------------------+  ← Common Header (12 bytes)
| Source Port        |
| Destination Port   |
| Verification Tag   |
| Checksum (CRC32c)  |
+--------------------+
| Type = 0x00 (DATA) |  ← Chunk Header
| Flags (e.g., B,E)  |
| Length             |
| TSN                |  ← Data Chunk Payload Header
| Stream ID          |
| Stream Seq No      |
| Payload Proto ID   |
| User Data          |
+--------------------+
```

## Full SCTP Packet Diagram

This example shows a packet with a **Common Header**, followed by an **INIT chunk** and a **HEARTBEAT chunk** — both control chunks.
```java
+---------------------------------------------------+
|                    Common Header                  |
|---------------------------------------------------|
| Source Port (2 bytes)                             |
| Destination Port (2 bytes)                        |
| Verification Tag (4 bytes)                        |
| Checksum (CRC32c) (4 bytes)                       |
+---------------------------------------------------+
|                   INIT Chunk                      |
|---------------------------------------------------|
| Chunk Type: 0x01 (INIT) (1 byte)                  |
| Flags: 0 (1 byte)                                 |
| Chunk Length (2 bytes)                            |
| Initiate Tag (4 bytes)                            |
| Advertised Receiver Window Credit (4 bytes)       |
| Num Outbound Streams (2 bytes)                    |
| Num Inbound Streams (2 bytes)                     |
| Initial TSN (4 bytes)                             |
| Optional Parameters (Variable)                    |
+---------------------------------------------------+
|                HEARTBEAT Chunk                    |
|---------------------------------------------------|
| Chunk Type: 0x04 (HEARTBEAT) (1 byte)             |
| Flags: 0 (1 byte)                                 |
| Chunk Length (2 bytes)                            |
| Heartbeat Info TLV (e.g., timestamp, IP)          |
+---------------------------------------------------+
```

---
# Summary

**SCTP** is a powerful, reliable transport protocol that:
- Combines the best of TCP and UDP
- Adds unique features like multi-streaming and multi-homing
- Is ideal for telecom, signaling, and critical systems

But it’s still **niche** and not as widely adopted as TCP or UDP.

