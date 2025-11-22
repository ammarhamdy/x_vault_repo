
The `hciconfig` command is a tool used to configure Bluetooth devices (specifically HCI – Host Controller Interface – devices). 

It is part of the **`BlueZ`** Bluetooth stack, which is the default Bluetooth protocol stack for Linux.

However, it's important to note that **`hciconfig` is deprecated** and is no longer maintained or included by default in some newer versions of BlueZ (post version 5.44). It has been largely replaced by **`bluetoothctl`** and **`btmgmt`**.


---
# What `bluetoothctl` Can Do

- Turn the Bluetooth adapter on or off
- Make the device discoverable or pairable
- Scan for nearby Bluetooth devices
- Pair, connect, and trust devices
- Remove devices
- Monitor connection status in real-time

---

**Start the tool**
```sh
bluetoothctl
```
This opens an interactive shell with a prompt

**Make the device discoverable and pairable**
```sh
agent on
default-agent
discoverable on
pairable on
```

**Scan for devices**
```sh
scan on
```

**Pair with a device**
```sh
pair 00:1A:7D:DA:71:13
```

**Trust the device (auto-connect on future boots)**
```sh
trust 00:1A:7D:DA:71:13
```

 **Connect to the device**
```bash
connect 00:1A:7D:DA:71:13
```

**Remove a device**
```bash
remove 00:1A:7D:DA:71:13
```

---
# Checking Status

**List paired devices:**
```bash
paired-devices
```

**Show Bluetooth controller status:**
```bash
show
```


---
# Summary

| Command         | Purpose                         |
| --------------- | ------------------------------- |
| `power on`      | Turn on the Bluetooth adapter   |
| `agent on`      | Enable the agent for pairing    |
| `scan on`       | Start scanning for devices      |
| `pair <MAC>`    | Pair with a device              |
| `connect <MAC>` | Connect to a device             |
| `trust <MAC>`   | Trust device for auto-reconnect |
| `remove <MAC>`  | Remove a paired device          |
