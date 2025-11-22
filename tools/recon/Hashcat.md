
https://hashcat.net/hashcat/

---

```bash
sudo apt install hashcat -y
```

**`Hashcat`** is one of the most powerful password recovery tools available.

**`Hashcat`** is a **fast and flexible password recovery tool** designed to **crack password hashes** using various attack methods. 

It's used by security professionals, penetration testers, and ethical hackers to audit password security.

Supports over 300 hash types (`MD5`, `SHA-1`, `bcrypt`, `NTLM`, etc.)

Leverages CPU and GPU acceleration (NVIDIA & AMD)


---

# Common Use Example

Let's say you have an **MD5 hash** like:
```
5f4dcc3b5aa765d61d8327deb882cf99
```
Which is the hash for `"password"`.

**Save hash to a file**
```bash
echo "5f4dcc3b5aa765d61d8327deb882cf99" > hash.txt
```

**Crack it using a dictionary**
```bash
hashcat -m 0 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```
* `-m 0`: Hash mode 0 (MD5)
* `-a 0`: Attack mode 0 (dictionary attack)
* `hash.txt`: File with hash
* `rockyou.txt`: Popular wordlist


* * *

# ⚔️ Attack Modes

| Mode | Description |
| --- | --- |
| `-a 0` | Dictionary attack |
| `-a 1` | Combinator (word1 + word2) |
| `-a 3` | Brute-force with masks |
| `-a 6` | Dictionary + mask hybrid |
| `-a 7` | Mask + dictionary hybrid |

* * *

# 🧠 Hash Modes (Examples)

| Hash Type | Mode # |
| --- | --- |
| MD5 | `0` |
| SHA1 | `100` |
| SHA256 | `1400` |
| bcrypt | `3200` |
| NTLM (Windows) | `1000` |
| WPA/WPA2 | `22000` |
Full list: `hashcat --help`

---

#  Tips

* Run `hashcat -I` to detect and use your GPU
* Use `--force` if testing in a VM or unsupported hardware
* For long runs, use `--restore` to resume interrupted sessions
    