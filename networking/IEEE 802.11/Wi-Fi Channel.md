
See: https://www.youtube.com/watch?v=dmODwteO0tw

In Wi-Fi (**IEEE 802.11**), a **channel** is basically a **specific slice of the radio frequency (RF) spectrum نطاق** that an **Access Point (AP)** uses to communicate with stations (STAs).


A **channel in the AP** is the specific frequency range the AP uses to talk to clients. 

Think of it like the "radio station" the AP is broadcasting on — all connected devices must tune in to the same station to communicate.

----

A Wi-Fi channel is ==a specific frequency range within a Wi-Fi band that routers and devices use to transmit data==.

Choosing the right channel is crucial for optimizing network performance, minimizing interference, and avoiding network congestion, especially in areas with many neighboring Wi-Fi networks.

Wi-Fi bands and their channels

Most modern Wi-Fi routers operate on the 2.4 GHz, 5 GHz, and 6 GHz bands. 

Each band has a different number of channels and unique characteristics.

----
# What is a Wi-Fi Channel?

The frequency band (like 2.4 GHz, 5 GHz, 6 GHz) is divided into smaller chunks, called channels.

Each channel is like a "==lane on a highway==" where data packets travel.

The AP chooses a channel, and all stations connected to it must use the same one.


# Channel Width

Defines how much spectrum نطاق the channel occupies يشغل: 

+ 20 MHz → default (most common, less interference).

+ 40 MHz, 80 MHz, 160 MHz → used in newer Wi-Fi (`802.11n`/`ac`/`ax`) for higher speeds but more interference.

## Example:
- In **2.4 GHz band**, channels are 20 MHz wide and overlap. Non-overlapping: **1, 6, 11**.

- In **5 GHz band**, there are many non-overlapping 20 MHz channels.

- In **6 GHz band (`Wi-Fi 6E/7`)**, even more spectrum is available with lots of clean channels.


# Why Channels Matter

If two nearby APs use the same channel, they **interfere** يتدخل and reduce performance.

Good network design = APs use different channels to **avoid overlap**.

Some APs automatically select the least congested channel.

![[e4d63bf8-9769-4e54-9ec9-852950d64694.png]]

Here’s the **2.4 GHz Wi-Fi channel map**:

- Each rectangle shows the frequency range of a channel (20 MHz wide).

- Channels **overlap heavily**, except for **1, 6, and 11** (highlighted in green), which are the **non-overlapping channels** typically used to minimize interference.

----
# 2.4 GHz band

![[Pasted image 20250828155647.png]]
https://www.linkedin.com/pulse/understanding-24ghz-5ghz-wifi-bands-channels-g-m-mahadi-hasan-mwntc/

- **Channels:** This band النطاق has 14 channels, but only 11 are available for use in the US. Due to channel overlap, only channels **1, 6, and 11** are considered non-overlapping and are the best for avoiding interference.
- **Characteristics:**
    - Offers a longer range and is better at penetrating walls and other objects than the 5 GHz band.
    - Prone to congestion ازدحام and interference تدخل because many other household devices, like microwaves, Bluetooth, and cordless phones, also use this band.
    - Has a ==lower maximum speed== compared to the 5 GHz band.


# 5 GHz band

- **Channels:** This band offers more channels and more non-overlapping options than the 2.4 GHz band, reducing the likelihood of interference.
- **Characteristics:**
    - Provides higher data rates and faster speeds but over a shorter range.
    - Because the shorter, faster waves do not penetrate walls as well, it works best when devices are closer to the router.
    - Features include wider channels (40, 80, and 160 MHz) and Dynamic Frequency Selection (DFS) to avoid radar interference.

# 6 GHz band

- **Channels:** Introduced with Wi-Fi 6E, this band is over twice as wide as the 5 GHz band, providing more high-speed, non-overlapping channels.
- **Characteristics:**
    - Delivers the fastest speeds and lowest latency of all bands.
    - Requires a newer router and a device that both support Wi-Fi 6E.
    - Has the shortest range and is most affected by obstructions.

---
# Commands to know your channel

```
iwconfig
```

```
sudo iwlist scan
```

```
nmcli dev wifi
```