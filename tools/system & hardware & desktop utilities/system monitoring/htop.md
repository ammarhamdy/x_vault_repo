
**`htop`** is an **interactive system-monitoring tool** for Unix-based systems (Linux, macOS, etc.), often used by developers, sysadmins, and DevOps engineers to view and manage system resource usage in real time.

It’s like a modern, user-friendly alternative to the classic `top` command, with more features and a better interface.

```bash
sudo apt  install htop
```

---
# Key Features of `htop`

|Feature|Description|
|---|---|
|**Real-time monitoring**|CPU, memory, swap, load average, uptime, etc.|
|**Color-coded display**|Easy-to-read CPU/memory usage bars.|
|**Interactive**|Use arrow keys, mouse, or shortcuts to navigate.|
|**Process management**|Kill, renice, trace, or filter processes.|
|**Multiple CPU core views**|Shows usage per core in parallel.|
|**Tree view**|Visualize process hierarchy (parent/child).|


---
# Examples

## Show only processes by a specific user:
```bash
htop -u username
```

----
# 🆚 `htop` vs `top`

|Feature|`htop`|`top`|
|---|---|---|
|Interface|Colorful, interactive|Text-only, basic|
|Navigation|Mouse + keyboard|Keyboard only|
|Process management|Easy (F9 to kill, arrows to select)|More manual|
|CPU core display|Separate bars|Single aggregate or flat|
|Configurable|Yes, via `F2`|Limited|