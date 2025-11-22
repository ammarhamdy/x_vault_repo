
https://www.kali.org/tools/rebind/

---
# Rebinding Attack

## What is a Rebinding Attack?

A **DNS Rebinding attack** is a technique where an attacker tricks a victim’s web browser into breaking the same-origin policy and making requests to internal or private network services that are normally not accessible from the internet.


## How It Works (Simplified)

1. **Attacker sets up a malicious domain** (e.g., `evil.com`).
    
2. The victim visits `evil.com`.
    
3. The attacker’s DNS server gives a short TTL (time-to-live) so that the browser will re-resolve the domain soon.
    
4. On the next lookup, the attacker’s DNS server returns a **different IP address**, this time pointing to a **private/internal IP** (e.g., `192.168.x.x`).
    
5. The browser thinks it’s still communicating with the same origin (`evil.com`), but is actually sending requests to a **device on the victim’s local network** (router, printer, database, etc.).
    
6. The attacker’s script running in the victim’s browser can now interact with internal services.


## What Attackers Can Do

- Access a home router’s admin panel.
    
- Scan the internal network.
    
- Exploit APIs of IoT devices, databases, or web servers inside private networks.
    
- Exfiltrate data.

## How to Defend Against It

- **Browser-level defenses**: Modern browsers restrict DNS rebinding in many cases.
    
- **Network defenses**:
    - Configure firewalls to block private IP access from untrusted sources.
    - Disable or restrict DNS responses with private IPs.
        
- **Application defenses**:
    - Require authentication for internal web apps.
    - Use CSRF tokens and strict origin checks.
        
- **Router defenses**: Many home routers include anti-rebinding protection.


----

```sh
rebind -i eth0 -d kali.local
```