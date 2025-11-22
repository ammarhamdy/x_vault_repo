
In **IEEE 802.11 (Wi-Fi)**, **RTS/CTS** stands for **Request to Send / Clear to Send**.  

It’s a **handshaking mechanism** at the **MAC layer** to reduce **collisions** in wireless communication.

**In short:** RTS/CTS is like raising your hand (RTS) and getting permission (CTS) before speaking in a crowded room, so that everyone knows when the air is reserved.

![[Pasted image 20250828170130.png]]

---
# Why RTS/CTS is Needed

Unlike wired Ethernet (where collisions can be detected directly), Wi-Fi devices can’t always "hear" each other because of:

- **Hidden Node Problem:**  
    Example: Two laptops at opposite corners of a room can both "see" the Access Point (AP) but not each other. They might transmit at the same time, causing a collision at the AP.
    
- **Exposed Node Problem:**  
    A device may unnecessarily stay silent even when its transmission wouldn’t interfere.
    
To solve these, RTS/CTS is used.


# How RTS/CTS Works

1. **RTS (Request to Send):**
    - A station (STA) that wants to transmit sends an **RTS frame** to the AP.
    - It includes how long it wants to use the channel.
        
2. **CTS (Clear to Send):**
    - The AP responds with a **CTS frame** if the channel is free.
    - This CTS is broadcast so all nearby stations know the medium will be busy for that duration.
        
3. **Data Transmission:**
    - The requesting STA sends the actual data.
        
4. **Acknowledgment (ACK):**
    - AP confirms reception with an ACK.


# Benefits

- Prevents collisions caused by hidden nodes.

- Improves reliability in congested networks.

- Ensures fairer medium access.


# Drawbacks

- Adds **extra overhead** (RTS + CTS frames before data).
    
- Not used for every transmission — typically only when packet size is large or in dense environments.