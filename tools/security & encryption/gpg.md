
The `gpg` command is used to manage **GPG (GNU Privacy Guard)** keys, which are part of a public-key cryptography system used to verify and sign software packages, ensuring they come from a trusted source.

---

# In the Context of Installing `k6`

When you install `k6` from Grafana’s APT repository, you need to ==trust their package signing key==.

That’s where the `gpg` command comes in.

**Here’s what this command does:**
```bash
curl -s https://dl.k6.io/key.gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/k6.gpg
```
+ `curl -s https://dl.k6.io/key.gpg`	Downloads the `GPG` key file from the official `k6` site
+ `gpg --dearmor`    Converts it from ASCII-armored format (text) to binary format
+ `-o /etc/apt/trusted.gpg.d/k6.gpg`	Saves the key in the directory where APT looks for trusted keys

APT uses that key to verify that packages downloaded from the `k6` repo were **signed by the official maintainers**, preventing tampering.

**To list trusted APT keys:**
```bash
apt-key list
```

**To list GPG keys in the new location (`/etc/apt/trusted.gpg.d/`):**
```bash
ls /etc/apt/trusted.gpg.d/
```

