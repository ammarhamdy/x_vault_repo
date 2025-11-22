https://currentmillis.com/
----


# [How to get the current time in milliseconds](https://currentmillis.com/#methods)

Methods to get the time in milliseconds since the UNIX epoch (January 1, 1970 00:00:00 UTC) in various programming languages:

```Bash	
date +%s%N | cut -b 1-13
```
`%s` ->  seconds since the Epoch (1970-01-01 00:00 UTC).
`%N` -> nanoseconds (000000000..999999999).
`cut -b 1-13` -> select only these bytes from `1` to `13`.


```java
System.currentTimeMillis()
```

```js
Date.now()
```



---


# [**What is a UNIX timestamp?**](https://currentmillis.com/tutorials/system-currentTimeMillis.html#unix-timestamp)

A UNIX timestamp, also known as _Epoch Time_ or _POSIX timestamp_, is a representation of a moment defined as the time that has elapsed since a reference known as the [UNIX epoch: 1970-01-01 00:00:00 UTC](https://currentmillis.com/?0).

Using Java as an example, `System.currentTimeMillis()` returns just that.

One of the most important things to realize is that 2 persons calling `System.currentTimeMillis()` at the same time should get the same result no matter where they are one the planet


----


# [**What is UTC?**](https://currentmillis.com/tutorials/system-currentTimeMillis.html#utc)

```sh
date -u
```

UTC is the main universal time keeping standard. 

It stands for _Coordinated Universal Time_. 

People use it to measure time in a common way around the globe (الكرة الأرضية). 

Since it is essentially being used interchangeably with GMT (Greenwich Mean Time) (بتوقيت غرينيتش) you could think of it as the timezone defined around the Greenwich Meridian a.k.a. the _Prime Meridian_ (0° longitude) (خط غرينتش المعروف أيضًا باسم خط الطول الرئيسي):

![[Pasted image 20250414104958.png]]


---


# Time zone

A **time zone** is a region of the world that uses the same standard time.

Because the Earth rotates, different parts of the world experience daylight and darkness at different times. 

To keep things organized, the world is divided into time zones—usually about every 15 degrees of longitude (which works out to 24 time zones for the 24 hours in a day).

Each time zone is usually an offset from **Coordinated Universal Time (UTC)**. 

For example:
- **UTC+0** is the time at the Prime Meridian (خط الطول الرئيسي) (like in London).
- **UTC+5** is 5 hours ahead of UTC (like in Pakistan).
- **UTC−8** is 8 hours behind UTC (like in parts of the U.S. West Coast).

So, when someone asks “what time zone are you in?” they’re really asking: _What standard time do you follow based on where you are in the world?_

​We're currently in **Eastern European Time (EET)**, which is **UTC+2**. 
This is Egypt's standard time zone.


## Daylight Saving Time

Starting **Friday, April 25, 2025**, Egypt will begin observing **Daylight Saving Time (DST)**. 

At midnight, clocks will move forward one hour to **UTC+3**, known as **Egypt Daylight Time (EEST)**. 

This adjustment helps make better use of daylight during the longer summer days.


## Get the time in other countries using Bash

### Using `TZ` environment variable (built-in, no extra tools).

You can temporarily set the time zone for the `date` command like this:
```sh
TZ="America/New_York" date
TZ="Asia/Tokyo" date
TZ="Europe/London" date
```

### Using `timedatectl` (Linux systems with `systemd`)

To list all available time zones:
```sh
timedatectl list-timezones
```

To check the current time zone of your system:
```sh
timedatectl
```

### Using `zdump` command

```sh
zdump Europe/Paris
zdump Asia/Dubai
```



---


# Real-Time Clock Time (**RTC time**) 


It refers to the time kept by a special hardware clock on your computer's motherboard. 

This clock continues running even when your computer is turned off, thanks to a small battery (like a CMOS battery).

## what’s it used for?
- When you turn your computer on, the **BIOS/UEFI** reads the time from the **RTC**.
- Then, the operating system can adjust or sync it (usually with internet time servers if available).
- The OS can set the RTC to either **local time** or **UTC**, depending on your system settings.


**To check RTC time in Linux:**

```sh
sudo apt install util-linux-extra
```

```sh
sudo hwclock --show
```


---


# Network Time Protocol (**NTP**)

It’s a **network protocol** used to **synchronize the clock** of your computer or device with a reliable time source over the internet (or a local network).

## Why is NTP important?
- Keeps your system clock **accurate**.    
- Makes sure time-sensitive operations (like logs, scheduled jobs, certificates, etc.) are all aligned.
- Prevents time drift that can happen if your system only uses the hardware clock (RTC), which can slowly become inaccurate.


## How does it work?
Your system connects to **NTP servers**, which are like "official clocks" on the internet. 

These servers get their time from very accurate sources, like:
- **Atomic clocks**
- **GPS clocks**

Your system checks in with them regularly and makes small corrections to your local clock to stay on time.


## On Linux, you can check NTP like this:

Using `systemd-timesyncd` (common in Ubuntu):
```sh
>> timedatectl status
               Local time: Mon 2025-04-14 11:37:36 EET
           Universal time: Mon 2025-04-14 09:37:36 UTC
                 RTC time: Mon 2025-04-14 09:37:36
                Time zone: Africa/Cairo (EET, +0200)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```
It’ll show you if NTP is active and synchronized.


