**`openssl`** is the Swiss army knife for SSL/TLS, certificates, and cryptography.

---
# Check SSL/TLS of a Server

## Connect to a server and show its certificate:
```sh
openssl s_client -connect example.com:443
```

## Quick check with SNI (Server Name Indication) ==important for sites with multiple domains==:
```sh
openssl s_client -connect example.com:443 -servername example.com
```


# View a Certificate File
```sh
openssl x509 -in cert.pem -text -noout
```


# Generate a Private Key

## RSA 2048-bit key:
```sh
openssl genrsa -out private.key 2048
```

## ECDSA key (smaller & faster):
```sh
openssl ecparam -genkey -name prime256v1 -out private.key
```

# Generate a Certificate Signing Request (CSR)

A CSR is what you send to a **Certificate Authority (CA)**:
```sh
openssl req -new -key private.key -out request.csr
```
It will ask questions:
- Country, State, Org Name
- Common Name (CN) → the domain name (e.g., `example.com`)

# Create a Self-Signed Certificate (for testing)
```sh
openssl req -x509 -new -nodes -key private.key -sha256 -days 365 -out selfsigned.crt
```
This makes a certificate valid for 365 days


# Convert Between Formats
## `PEM` → `DER`:
```sh
openssl x509 -in cert.pem -outform der -out cert.der
```
## `DER` → `PEM`:
```sh
openssl x509 -in cert.der -inform der -out cert.pem
```
## `PEM` → `PKCS#12` (`.pfx`):
```sh
openssl pkcs12 -export -out cert.pfx -inkey private.key -in cert.pem -certfile chain.pem
```


# Test Available Protocols
```sh
openssl s_client -connect example.com:443 -tls1_2
```

# Verify a Certificate
Check if cert is valid with a CA chain:
```sh
openssl verify -CAfile chain.pem cert.pem
```

---
# 🔐 OpenSSL Cheat Sheet

## 🔎 1. Check Servers
```bash
# Connect to server and show cert
openssl s_client -connect example.com:443

# With SNI (for virtual hosts)
openssl s_client -connect example.com:443 -servername example.com

# Force TLS version
openssl s_client -connect example.com:443 -tls1_2
openssl s_client -connect example.com:443 -tls1_3
```

## 📜 2. View Certificates
```bash
# View PEM certificate details
openssl x509 -in cert.pem -text -noout

# Check certificate validity
openssl x509 -in cert.pem -noout -dates

# Verify certificate against CA
openssl verify -CAfile chain.pem cert.pem
```

## 🔑 3. Generate Keys
```bash
# RSA 2048-bit private key
openssl genrsa -out private.key 2048

# ECDSA private key
openssl ecparam -genkey -name prime256v1 -out private.key
```

## 📝 4. Create CSR (Certificate Signing Request)
```bash
# Generate CSR from key
openssl req -new -key private.key -out request.csr

# Generate CSR with config (no prompts)
openssl req -new -key private.key -out request.csr -subj "/CN=example.com/O=MyOrg/C=US"
```

## 🔒 5. Self-Signed Certificate
```bash
openssl req -x509 -new -nodes -key private.key -sha256 -days 365 -out selfsigned.crt
```

## 🔄 6. Convert Certificate Formats
```bash
# PEM → DER
openssl x509 -in cert.pem -outform der -out cert.der

# DER → PEM
openssl x509 -in cert.der -inform der -out cert.pem

# PEM + key → PFX/P12
openssl pkcs12 -export -out cert.pfx -inkey private.key -in cert.pem -certfile chain.pem

# PFX → PEM
openssl pkcs12 -in cert.pfx -out cert.pem -clcerts -nokeys
openssl pkcs12 -in cert.pfx -out private.key -nocerts -nodes
```

## 🔧 7. Misc Tools
```bash
# Check hash of a file
openssl dgst -sha256 file.txt

# Encrypt/Decrypt file with AES-256
openssl enc -aes-256-cbc -in plain.txt -out encrypted.bin
openssl enc -d -aes-256-cbc -in encrypted.bin -out plain.txt
```
