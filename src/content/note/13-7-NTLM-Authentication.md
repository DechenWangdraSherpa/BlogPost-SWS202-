---
title: 13-7-NTLM Authentication 
seriesId: 13-Active-Directory
publishDate: "2025-04-29T15:12:00Z"
---

# NTLM Authentication Overview

Active Directory (AD) uses various authentication methods, including LM, NTLM, NTLMv1, NTLMv2, and Kerberos. NTLM, in particular, has become the standard for many Windows systems, though Kerberos is preferred where possible due to its stronger security features. Understanding the differences between these authentication methods is crucial, as they each have distinct strengths and vulnerabilities. Here's a comparison of the various hashes and protocols:

## Hash/Protocol Comparison

| Hash/Protocol  | Cryptographic Technique   | Mutual Authentication | Message Type       | Trusted Third Party |
|----------------|----------------------------|-----------------------|--------------------|---------------------|
| **NTLM**       | Symmetric key cryptography  | No                    | Random number      | Domain Controller   |
| **NTLMv1**     | Symmetric key cryptography  | No                    | MD4 hash, random number | Domain Controller   |
| **NTLMv2**     | Symmetric key cryptography  | No                    | MD4 hash, random number | Domain Controller   |
| **Kerberos**   | Symmetric & asymmetric cryptography | Yes                | Encrypted ticket (DES, MD5) | Domain Controller/KDC |

## LM (LAN Manager) Hashes

- **Introduction**: The LM hash is the oldest password storage mechanism used in Windows, introduced in 1987. It was replaced by NTLM due to significant security weaknesses.
- **Limitations**: 
  - Passwords are limited to 14 characters.
  - They are case-insensitive and converted to uppercase.
  - The hash is based on splitting the password into two 7-character chunks, with weak security due to the use of DES encryption.
  - **Vulnerability**: The LM hash can be cracked easily using tools like **Hashcat**, as it can be brute-forced in a short time, especially for passwords less than 7 characters.

## NTLM (NT LAN Manager)

- **NTLM Hash**: NTLM uses the **MD4 hash** of the UTF-16 little-endian password string. This is stronger than the LM hash but still has weaknesses.
- **Challenge-Response Process**:
  - A client sends a **NEGOTIATE_MESSAGE** to the server.
  - The server responds with a **CHALLENGE_MESSAGE**.
  - The client responds with an **AUTHENTICATE_MESSAGE**.
- **Cracking**: NTLM hashes can still be cracked using tools like **Hashcat**, but the process is slower compared to LM hashes, and the complexity increases with longer passwords.
- **Vulnerability**: NTLM is vulnerable to **Pass-the-Hash** (PtH) attacks, where attackers can use the hash without needing the plaintext password.

## NTLMv1 (Net-NTLMv1)

- **NTLMv1** uses both the **NT** and **LM hashes** in its challenge/response process, making it easier to crack.
- **Challenges**: Vulnerable to **NTLM relay attacks** and weak against modern attack techniques.
- **Common Attack**: Capturing the NTLMv1 hash using tools like **Responder** or via **NTLM relay** attacks can expose credentials without the need for a full password crack.

## NTLMv2 (Net-NTLMv2)

- **NTLMv2** improves upon NTLMv1 by introducing stronger cryptographic mechanisms.
- **Response Process**: Sends two responses to an 8-byte challenge: 
  - The first response is an **HMAC-MD5** hash of the challenge and a client-generated value.
  - The second response includes a **client challenge** and the domain name.
- **Improved Security**: NTLMv2 is resistant to certain spoofing attacks that affect NTLMv1 and provides better protection against relay attacks.
- **Deployment**: NTLMv2 is the default in modern Windows systems (since **Windows NT 4.0 SP4**).

## Domain Cached Credentials (DCC)

- **MSCache2** (Domain Cached Credentials) is used to store hashes locally on a domain-joined machine.
- **Purpose**: Helps users log in to a machine when it cannot communicate with the domain controller (e.g., due to a network outage).
- **Storage**: The last 10 user hashes are stored in the **HKEY_LOCAL_MACHINE\SECURITY\Cache** registry key.
- **Cracking**: Cracking DCC hashes is slow and difficult, requiring specific tools like **Hashcat**. However, these hashes cannot be used in **Pass-the-Hash** attacks.

---

## Summary

1. **LM Hash**: Obsolete, insecure, and easily cracked.
2. **NTLM**: More secure than LM but vulnerable to **Pass-the-Hash** and **brute-forcing**.
3. **NTLMv1**: More secure than LM but still vulnerable to **relay attacks**.
4. **NTLMv2**: The most secure version of NTLM with protections against spoofing and relay attacks, preferred in modern environments.
5. **Domain Cached Credentials**: Stored locally for offline use, can be targeted if an attacker gains access to the machine.

Understanding these authentication protocols and their vulnerabilities is critical for both defenders and attackers in Active Directory environments. Tools like **Hashcat** can crack these hashes, while **Pass-the-Hash** attacks exploit weak authentication setups.
