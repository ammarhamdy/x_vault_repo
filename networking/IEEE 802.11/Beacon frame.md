
In Wi-Fi (**IEEE 802.11**), a **beacon frame** is one of the most important **management frames**.

It is sent by an **Access Point (AP)** to announce the existence of a wireless network and provide essential information about it.

---

A beacon frame is ==a special type of management frame in IEEE 802.11 Wi-Fi networks that an access point (AP) periodically transmits to announce its presence and advertise network information==. 

These frames contain details about the Wi-Fi network's capabilities, security, and configuration, allowing nearby devices to discover the network, identify it, and connect to it. Beacon frames are essential for network synchronization and help mobile devices find and join networks without a prior connection.

---

A **beacon frame** is like a **Wi-Fi network’s advertisement billboard**. It repeatedly broadcasts the network’s name, channel, and capabilities so that devices know it exists and can connect.

---
# What is a Beacon Frame?

A **periodic broadcast message** from an AP (usually every 100 ms).

Tells all nearby devices:
> “Hi, I’m AP `Home_Network`, here are my details if you want to join!”

Without beacon frames, devices would have a hard time discovering Wi-Fi networks.

---
# What Information is Inside a Beacon Frame?

A beacon frame contains:

1. **SSID (Service Set Identifier):** The network name (e.g., `Home_WiFi`).
    
2. **BSSID:** The MAC address of the AP.
    
3. **Supported Data Rates:** (e.g., 802.11n, 802.11ac).
    
4. **Channel/Frequency:** Which channel the AP is using.
    
5. **Security Information:** WEP, WPA2, WPA3, etc.
    
6. **Timestamp:** For time synchronization.
    
7. **Capabilities:** Whether AP supports features like short preamble, QoS, etc.

---
# Beacon Frame & Probe Request/Response

**Beacon frame:** Sent **periodically** by the AP (broadcast).

**Probe request:** Sent by a **station** (client) to ask about networks.

**Probe response:** Sent by AP in reply to a probe request.

👉 So, **beacon = passive discovery**, while **probe = active discovery**.



![[Pasted image 20250828165952.png]]

- The **AP periodically sends beacon frames** (advertising its SSID, channel, and security settings).

- The **STA (station, e.g., laptop/phone) can send a probe request** (“Any AP here?” or for a specific SSID).

- The **AP replies with a probe response**, confirming its details.


👉 Devices can discover networks in **==two ways==**:
- **Passive scanning:** Listening to beacon frames.
- **Active scanning:** Sending probe requests and waiting for probe responses.