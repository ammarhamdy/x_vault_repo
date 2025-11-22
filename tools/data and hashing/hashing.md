


----

| Algorithm      | Security             | Speed        | Best For                     |
| -------------- | -------------------- | ------------ | ---------------------------- |
| **MD5**        | ❌ Weak               | ⚡ Fast       | Checksums, basic hashing     |
| **SHA-1**      | ❌ Weak               | ⚡ Fast       | Legacy systems               |
| **SHA-256**    | ✅ Secure             | 🔥 Moderate  | Cryptography, blockchain     |
| **SHA-512**    | ✅ Secure             | 🔥 Moderate  | High-security applications   |
| **SHA-3**      | ✅✅ Very Secure       | ⏳ Slower     | Cryptographic security       |
| **BLAKE2**     | ✅ Secure             | ⚡ Fast       | Cryptography, secure hashing |
| **Bcrypt**     | ✅✅ Very Secure       | 🐌 Slow      | Password hashing             |
| **Argon2**     | ✅✅✅ Extremely Secure | 🐌 Slow      | Modern password hashing      |
| **CRC32**      | ❌ Not Secure         | ⚡⚡ Very Fast | Checksums                    |
| **RIPEMD-160** | ✅ Secure             | 🔥 Moderate  | Cryptographic use            |
| **Whirlpool**  | ✅✅ Very Secure       | ⏳ Slower     | High-security hashing        |

---
# Hex, binary, byte

1 byte --> 2 hex --> 8 bits 

**Bits**
1 byte -> 8 bits
1 hex -> 4 bits



-----
## MD5 (Message Digest Algorithm 5)
- **Output Size:** 128-bit (32-character hex) `128/4=32`
- **Speed:** Fast
- **Use Case:** Checksums, data integrity verification
- **Security:** **Not secure** (Vulnerable to collisions & brute force attacks)

```MD5
HelloWorld → fc3ff98e8c6a0d3087d515c0473f8677
peter      → e10adc3949ba59abbe56e057f20f883e
```

---
## SHA-1 (Secure Hash Algorithm 1)
- **Output Size:** 160-bit (40-character hex) `160/4=40`
- **Speed:** Fast
- **Use Case:** Digital signatures, SSL certificates (legacy)
- **Security:** **Not secure** (Prone to collision attacks)

```SHA-1
HelloWorld → 2ef7bde608ce5404e97d5f042f95f89f1c232871
```


---
## SHA-2 (Secure Hash Algorithm 2)
- **Variants:** SHA-224, SHA-256, SHA-384, SHA-512
- **Output Size:**
    - SHA-256 → 256-bit (64-character hex)
    - SHA-512 → 512-bit (128-character hex)
- **Speed:** Moderate
- **Use Case:** Password hashing, digital signatures, blockchain
- **Security:** **Secure** (No known practical attacks)

```SHA-256
HelloWorld → fc5e038d38a57032085441e7fe7010b0d5e17a2fc12b1b9774c39e89bcda44b7
```


---
## SHA-3 (Keccak Algorithm)
- **Variants:** SHA3-224, SHA3-256, SHA3-384, SHA3-512
- **Output Size:** Same as SHA-2 variants
- **Speed:** Slower than SHA-2 but more secure
- **Use Case:** Cryptographic security, blockchain, secure applications
- **Security:** **Highly secure** (Designed to resist all known attacks)

---
# SHAKE
`shake_128` is a member of the **SHA-3** (Secure Hash Algorithm 3) family. It is different from **SHA-1** and **SHA-2** and is classified as an **Extendable-Output Function (XOF)**.

- **SHA-1 is obsolete** and no longer secure.
- **SHA-2 (SHA-256, SHA-512) is widely used but has a fixed output size.**
- **SHA-3 is the latest standard and is more secure than SHA-2.**
- **SHAKE-128 and SHAKE-256 are unique because you can generate a hash of any length** (useful for cryptographic applications like key derivation).


---
## BLAKE2 (BLAKE2b & BLAKE2s)
- **Output Size:** Customizable (up to 512-bit)
- **Speed:** Faster than SHA-3, comparable to SHA-2
- **Use Case:** Cryptographic hashing, password hashing
- **Security:** **Secure** (Considered a strong alternative to SHA-3)


---
## Bcrypt
- **Output Size:** 192-bit (Encrypted format, includes salt)
- **Speed:** **Slow on purpose** (Uses computational cost factor)
- **Use Case:** Password hashing (used in Unix/Linux, PHP, Django)
- **Security:** **Very secure** (Resistant to brute force attacks)

```bcrypt
$2a$12$D4G5f18o7aMMfwasBlS5uO7E2R.wDMN3X/Ybs28FK2IV1F6k6JxY2
```

---
## Argon2 (Winner of Password Hashing Competition)
- **Output Size:** Customizable
- **Speed:** Adjustable (Memory-hard to resist GPU/ASIC attacks)
- **Use Case:** Password hashing (Modern replacement for Bcrypt)
- **Security:** **Extremely secure** (Used in modern applications)


---
## CRC32 (Cyclic Redundancy Check)
- **Output Size:** 32-bit
- **Speed:** Very fast
- **Use Case:** Error checking, checksums (not for security)
- **Security:** **Not secure** (Easy to reverse)

```CRC32
HelloWorld → 8bd69e52
```


---
## RIPEMD (RACE Integrity Primitives Evaluation Message Digest)
- **Variants:** RIPEMD-128, RIPEMD-160, RIPEMD-256, RIPEMD-320
- **Output Size:** 128, 160, 256, 320-bit
- **Use Case:** Cryptographic applications
- **Security:** **RIPEMD-160 is considered secure**, older versions are weak


---
## Whirlpool
- **Output Size:** 512-bit
- **Speed:** Slower but highly secure
- **Use Case:** Cryptographic security, encryption software
- **Security:** **Very secure**


