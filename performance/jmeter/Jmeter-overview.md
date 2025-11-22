
![[Pasted image 20250505203516.png]]
- `Thread Group`: how many users.
- `Http Request`: what those users going to do.
- `View Result Tree`: the result.


---
# Assertions


Assertions are using for verification purpose, by comparing the actual result by the expected result.

Add assertion:![[Pasted image 20250506191443.png]]


---

# Thread group


![[Pasted image 20250509163337.png]]

1. `Number of Threads`: number of users that will access the target.
2. `Ramp-up period`: is the time frame in seconds for all threads (virtual users) to start. It tells JMeter how long to take to "ramp-up" to the full number of threads chosen.
3. `Loop Count`: How many times I will execute this scenario.

```
total requests = Number of Threads * Loop Count
```
 

---

# Test script recorder

## Generate certificate 

```bash
> cd /path/to/jmeter/bin
```

```bash
keytool -genkeypair -alias jmeter -keyalg RSA -keysize 2048 -keystore jmeter.jks -dname "CN=JMeter, OU=Test, O=Organization, L=City, ST=State, C=US" -validity 365
```
- `-alias jmeter`: The alias for the key pair.
- `-keyalg RSA`: The encryption algorithm.
- `-keysize 2048`: The size of the key.
- `-keystore jmeter.jks`: The output keystore file.
- `-dname`: The distinguished name details.
- `-validity 365`: The certificate's validity period (in days).

**You may need to export the public certificate from the keystore to distribute it.**
```sh
keytool -export -alias jmeter -keystore jmeter.jks -file jmeter.cer
```
This will generate a **`jmeter.cer`** file, which is the public certificate.


### Configuring JMeter to Use the Certificate
Go to **JMeter** and open **HTTPS Test Script Recorder**.
Under **"Global Settings"**, specify the keystore file path:
```
Keystore Configuration:
Keystore Path: /path/to/jmeter.jks
Password: changeit
```

### Importing Certificate to Browser (if acting as a proxy)
If you are using JMeter to capture HTTPS traffic, you need to **import the certificate** to your browser.
- Open **Browser Settings → Security → Manage Certificates**.
- Import the **`jmeter.cer`** file under **"Trusted Root Certification Authorities"**.



---



**Extract  `_toke` from `input`:**
![[Pasted image 20250510151303.png]]


**Use extracted token**
![[Pasted image 20250510151404.png]]