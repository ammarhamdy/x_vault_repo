

**Network Manager command-line tool**, It allows users to configure, control, and monitor network connections directly from the terminal.

**Show overall status:**
```
nmcli general status
```

**Check networking status:**
```
nmcli networking
```

## Device Management:

**List all devices:**
```
nmcli device
```

**Show detailed information about a specific device:**
```
nmcli device show wlo1
```

**Enable or disable a device:**
```
nmcli device connect wlo1
nmcli device disconnect wlo1
```

## Wi-Fi Management:

**List available Wi-Fi networks:**
```sh
nmcli device wifi list
```

**Connect to a Wi-Fi network:**
```sh
nmcli device wifi connect "SSID" password "your_password"
```

**Full Silent Command**:
```sh
sudo nmcli -s device wifi connect 8C:68:C8:9E:2A:04 password 123456789
```
**or**
```sh
sudo nmcli -s -g GENERAL.STATE device wifi connect "SSID" password "your_password" >/dev/null 2>&1
```
- `-s`: Shortens output (no prompt or interactive feedback).
- `-g GENERAL.STATE`: Optionally limit output (e.g., to state only).
- `>/dev/null 2>&1`: Redirects **stdout and stderr** to null to suppress **all output** (silent mode).
- If you don’t want **any feedback**, omit `-g GENERAL.STATE`.

**Forget a saved Wi-Fi connection:**
```sh
nmcli connection delete id "SSID"
```

## Connection Management:

**List all saved connections:**
```sh
nmcli connection show
```

**Activate a connection:**
```sh
nmcli connection up "connection_name"
```

**Deactivate a connection:**
```sh
nmcli connection down "connection_name"
```

