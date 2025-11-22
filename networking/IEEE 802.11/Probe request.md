
**probe requests** are an important part of how Wi-Fi (IEEE 802.11) works.

----
# What is a Probe Request?

A **probe request** is a **management frame** sent by a Wi-Fi device (station/STA — like your laptop or phone) to **discover nearby wireless networks**.

Think of it like your device “shouting”:
> “Hey, are there any Wi-Fi networks around? If yes, please tell me!”

---
# Types of Probe Requests

1. **Broadcast (Wildcard) Probe Request**
    - The device asks **all nearby Access Points (APs)** to reply.
    - Sent when you open the Wi-Fi list on your phone/laptop.
    - Example: “Any APs out there?”
        
2. **Directed Probe Request**
    - The device asks for a **specific SSID (network name)**.
    - Example: “Is `Home_Network` here?”
    - Used when your device remembers previously connected Wi-Fi networks.

Imagine you walk into a conference hall looking for friends:
- If you **shout “Is anyone here?”** → that’s a broadcast probe.
- If you **shout “Is Alice here?”** → that’s a directed probe.

---
# Who Responds?

Nearby APs that match the probe request will respond with a **probe response** frame.

The response contains details like SSID, supported data rates, security (`WPA`/`WPA2`), etc.


---
# Why Probe Requests Matter

They help devices quickly **find and connect** to Wi-Fi networks.

They reduce waiting time compared to passively listening for **beacon frames** from APs.

They also reveal **which networks a device has previously connected to** (because of directed probes).
- ⚠️ That’s why tools like **`Wifiphisher`** or other sniffers can see past SSIDs from probe requests → privacy risk.
