
The **`lshw`** command in Ubuntu is used to display detailed information about the **hardware configuration** of your system (CPU, RAM, disks, network interfaces, etc.).

----
# Common Options

| Command                                | Description                                                     |
| -------------------------------------- | --------------------------------------------------------------- |
| `sudo lshw -short`                     | Displays hardware in a **short summary** table.                 |
| `sudo lshw -html > hardware.html`      | Exports hardware details to an **HTML file** (view in browser). |
| `sudo lshw -json > hardware.json`      | Exports in JSON format.                                         |
| `sudo lshw -class processor`           | Show information about the **CPU(s)** only.                     |
| `sudo lshw -class memory`              | Show information about **RAM**.                                 |
| `sudo lshw -class network`             | Show network interfaces (Ethernet, Wi-Fi, etc.).                |
| `sudo lshw -class disk -class storage` | Show details of storage devices.                                |

# Get a compact overview
```sh
sudo lshw -short
```

# Get CPU details
```sh
sudo lshw -class processor
```
