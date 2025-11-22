
An **SSL certificate** (more accurately, a **TLS certificate**, since TLS is the modern version of SSL) is a **digital certificate** that provides **authentication** and **encryption** for a website.

**TLS** stands for **Transport Layer Security**.

**TLS** is a **cryptographic protocol** used to:
- Secure communication over a computer network
- Provide **encryption**, **authentication**, and **data integrity**

It is the **successor to SSL** (Secure Sockets Layer), and is more secure and modern.

---

# SSL vs. TLS

|Feature|SSL|TLS|
|---|---|---|
|Full Form|Secure Sockets Layer|Transport Layer Security|
|Status|Deprecated|Actively used & supported|
|Latest Version|SSL 3.0 (insecure)|TLS 1.3 (recommended)|
|Use Case|Was used for HTTPS|Powers HTTPS today|


---

# What Does an SSL Certificate Do?

1. **Encrypts data** between a user's browser and a website (protects login info, credit card numbers, etc.)
    
2. **Authenticates the website’s identity** (proves it’s legitimate, not a fake or malicious clone)
    
3. **Enables HTTPS** instead of HTTP — you’ll see the 🔒 padlock icon in browsers


# What’s Inside an SSL Certificate?

An SSL/TLS certificate contains:
- **Domain name** it’s issued for (e.g., `example.com`)
- **Organization** name (for verified businesses)
- **Certificate Authority (CA)** – the trusted third party that issued it (e.g., `DigiCert`, Let's Encrypt)
- **Expiration date**
- **Public key** (used in the encryption process)
- **Digital signature** from the CA

# How SSL Works (Simplified)

1. You visit `https://example.com` 

2. The website sends its SSL certificate to your browser

3. Your browser checks if it’s valid and issued by a trusted CA

4. If valid, they use it to create a secure (encrypted) connection

# Why SSL Matters

| Benefit               | Description                                     |
| --------------------- | ----------------------------------------------- |
| **Security**          | Protects sensitive data from hackers/sniffers   |
| **Trust**             | Users trust sites with HTTPS and the padlock    |
| **SEO Boost**         | Google favors HTTPS in search rankings          |
| **Prevents Warnings** | Browsers warn users if SSL is missing or broken |


# Types of SSL Certificates

|Type|Use Case|Verified Info|
|---|---|---|
|**DV (Domain Validation)**|Basic personal or blog sites|Only domain ownership|
|**OV (Org Validation)**|Business websites|Domain + business identity|
|**EV (Extended Validation)**|High-trust sites (e.g. banks)|Full legal verification (green bar or business name in browser)|


---
# # TLS Handshake (Simplified Flow)

1. Client connects to `https://example.com`.
2. Server sends its certificate.
3. Client verifies certificate (valid, trusted, not expired).
4. Both agree on encryption algorithms (cipher suites).
5. A session key is exchanged securely.
6. Encrypted communication begins.


---
# Example: SSL Certificate


```
openssl s_client -connect example.com:443 -showcerts
```

## Verbose 
```sh
curl -v 'https://codlopchat.xyz/auth/login'
```

## Output:
```
* Host codlopchat.xyz:443 was resolved.
* IPv6: 2606:4700:3037::6815:159e, 2606:4700:3032::ac43:c757
* IPv4: 172.67.199.87, 104.21.21.158
*   Trying 172.67.199.87:443...
* Connected to codlopchat.xyz (172.67.199.87) port 443
* ALPN: curl offers h2,http/1.1
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
* Recv failure: Connection reset by peer
* OpenSSL SSL_connect: Connection reset by peer in connection to codlopchat.xyz:443 
* Closing connection
```

## Step-by-step breakdown
```
* Host codlopchat.xyz:443 was resolved.
```
✅ DNS worked. 
Your system successfully resolved `codlopchat.xyz` to IPs.

```
* IPv6: 2606:4700:3037::6815:159e, 2606:4700:3032::ac43:c757
* IPv4: 172.67.199.87, 104.21.21.158
```
Those are Cloudflare IPs (so the domain is behind **Cloudflare’s CDN/WAF**).

```
*   Trying 172.67.199.87:443...
* Connected to codlopchat.xyz (172.67.199.87) port 443
```
TCP handshake succeeded. 
So the server is reachable at the network level.

```
* ALPN: curl offers h2,http/1.1
```
`curl` is saying: _I can talk HTTP/2 (`h2`) or HTTP/1.1_.

```
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
```
Your client sent a **`TLS ClientHello`** message to start the SSL handshake.

```
*  CAfile: /etc/ssl/certs/ca-certificates.crt
*  CApath: /etc/ssl/certs
```
These are your local root CAs — normal.

```
* Recv failure: Connection reset by peer
* OpenSSL SSL_connect: Connection reset by peer in connection to codlopchat.xyz:443
```
💥 Here’s the problem: as soon as your client started TLS negotiation, the **remote side (`Cloudflare` or the origin server)** forcibly closed the connection with a TCP RST packet.

```
* Closing connection
curl: (35) Recv failure: Connection reset by peer
```
Curl couldn’t complete TLS handshake, so it fails.

----
