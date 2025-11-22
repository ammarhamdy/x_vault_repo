
# What is SSH (Secure Shell)

It’s a cryptographic network protocol that lets you securely connect to another machine over an insecure network (like the Internet or a local LAN).

Main uses:
- Remote login (command line on a server).
- Secure file transfer (SCP, SFTP).
- Secure tunneling (forward ports, VPN-like tunnels).


---
# How does SSH work

1. **Connection setup**
    - You run: `ssh user@server`
    - Your SSH client contacts the SSH server on port **22** (by default).

2. **Server introduces itself (host key)**
    - The server says: _"Here’s my public host key."_
    - The client checks if it knows this key (via the `known_hosts` file).
    - If not, you get the authenticity warning.

3. **Secure channel setup (key exchange)**
    - Both sides agree on:
        - Which encryption algorithms to use (`AES`, `ChaCha20`, etc.).
        - How to generate a **shared secret** key using asymmetric cryptography (like `Diffie-Hellman`, `Curve25519`).
    - This creates an encrypted channel, so all communication after this point is protected from eavesdropping.

4. **Authentication of the user**
    - Now that the channel is secure, the server must verify _you_.
    - Methods:
        - **Password authentication**: you type your password.
        - **Public key authentication**: your client signs a challenge with your private key; the server checks it against your public key stored in `~/.ssh/authorized_keys`.
    - If authentication succeeds, you’re logged in as `user`.
    - To test whether a server allows password-based authentication use Nmap’s built-in NSE script `ssh-auth-methods.nse`

5. **Secure communication**
	- Every command you type and every response from the server is encrypted and protected from tampering.

# Example timeline of your session

```http
You: ssh user@172.16.10.13
Client: Connects → "Server, who are you?"
Server: Sends host key (ED25519).
Client: Doesn’t recognize → warns you → asks "Trust this fingerprint?"
You: yes
Client: Saves host key in ~/.ssh/known_hosts
Server: "Okay, now who are you?"
Client: Sends your username "user".
Server: "Prove it."
Client: Sends password (since no SSH key was used).
Server: Authenticated → opens shell.
```

---

```sh
ssh user@172.16.10.13
```

# The output
```
The authenticity of host '172.16.10.13 (172.16.10.13)' can't be established.
ED25519 key fingerprint is SHA256:c89YzVU+EW/2o+lZm30BgEjutZ0f2t145cSyX2/zwzU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
user@172.16.10.13's password:
```

# What is the key fingerprint

The fingerprint is a short, human-readable summary (a cryptographic hash) of a host’s **public key**.

**In the output message:**  
`ED25519 key fingerprint is SHA256:c89YzVU+EW/2o+lZm30BgEjutZ0f2t145cSyX2/zwzU.`  
That means the server presented an `ED25519` host key and the client computed its SHA-256 hash (displayed in `base64`) — the fingerprint.

**Purpose:** 
Fingerprints let you _verify_ you’re connecting to the same host you expect (and not a man-in-the-middle). 
If the fingerprint you see now matches one you previously recorded (or one the admin gave you out-of-band), the host is genuine.

**Common fingerprint formats:** 
`SHA256` (modern, preferred), older systems sometimes show MD5 (hex with colons).

# What is the **known_hosts** file?

`known_hosts` is where your SSH client stores the host keys (or fingerprints) of servers you’ve connected to so future connections can be checked automatically.

**Typical locations:**
- per-user: `~/.ssh/known_hosts`
- system-wide: `/etc/ssh/ssh_known_hosts`

What happens when you answer `yes` to that prompt: the client adds the server’s host key (or a hashed form of the hostname plus the key) to `~/.ssh/known_hosts`.
Next time, SSH compares the server’s key to the stored one; if they differ you’ll get a warning (possible MITM or server key changed).

**File details:**
- Each line: `hostnames keytype base64-encoded-key [comment]`
- Hostnames can be a name, IP, or a comma-separated list. They can also be stored hashed (starts with `|1|...`) for privacy.

**Useful commands:**
- show known_hosts lines for an IP: `ssh-keygen -F 172.16.10.13`
- remove an old entry: `ssh-keygen -R 172.16.10.13` (removes matching lines from `~/.ssh/known_hosts`)

# What is the **public key** (and how it differs from what you saw)?

SSH uses asymmetric key pairs: **private key** (kept secret) + **public key** (shared).

**There are two distinct uses of keys in SSH:**

1. **Host keys** (the server’s keypair). The server's **public host key** is what the client saw and whose fingerprint was shown. It proves the server’s identity. The corresponding server private host key stays on the server (e.g. `/etc/ssh/`).

2. **User keys** (your keypair for login). You put your _public_ user key on the server in `~/.ssh/authorized_keys` so you can authenticate without a password. Your private user key stays on your client machine.

The fingerprint in the prompt is derived from the **server’s public host key** (not from your user key).

If you want to use key-based login instead of a password, you generate an SSH keypair locally (`ssh-keygen`) and copy the public key to the server (`ssh-copy-id user@host` or put it in `~/.ssh/authorized_keys`).


# How to _verify_ the fingerprint safely

Always verify the fingerprint using an out-of-band channel (ask the admin, check the server console, check a known internal wiki):

Ask the server admin to provide the “`ED25519 SHA256:…` ” fingerprint and compare.

Or compute from the server’s public host key (on the server):  
`ssh-keygen -lf /etc/ssh/ssh_host_ed25519_key.pub`

Or compute remotely (unsafe vs MITM unless you trust the network):  
`ssh-keyscan -t ed25519 172.16.10.13 | ssh-keygen -lf -`  
If the presented fingerprint matches the verified fingerprint, accept and the client will add it to `~/.ssh/known_hosts`.


