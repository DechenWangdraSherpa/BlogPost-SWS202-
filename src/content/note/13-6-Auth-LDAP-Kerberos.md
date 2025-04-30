---
title: 13-6-Auth LDAP Kerberos 
seriesId: 13-Active-Directory
publishDate: "2025-04-29T14:50:00Z"
---

# Kerberos, DNS, LDAP, MSRPC in Active Directory

## Kerberos

Kerberos has been the default authentication protocol for domain accounts since Windows 2000. It is an open standard and allows for interoperability with other systems using the same standard. When a user logs into their PC, Kerberos is used to authenticate them via mutual authentication, where both the user and the server verify their identity.

### Key Points:
- **Stateless authentication** protocol based on tickets instead of transmitting user passwords over the network.
- **KDC (Key Distribution Center)**: Issues tickets for authentication.
- **Ticket Process**:  
  1. The user requests a **TGT (Ticket Granting Ticket)**.
  2. The user presents the **TGT** to request a **TGS (Ticket Granting Service)** ticket.
  3. The user presents the **TGS** to access a service.
  
#### Kerberos Authentication Flow:
1. The user logs in, and their password encrypts a timestamp, sent to the KDC.
2. The KDC decrypts the request and issues a **TGT** encrypted with the secret key of the `krbtgt` account.
3. The user presents the TGT to request a TGS for a specific service.
4. The KDC validates the TGT and provides the TGS encrypted with the service's NTLM password hash.
5. The user presents the TGS to the service for access.

Kerberos uses **port 88** (TCP/UDP). Tools like Nmap can help identify Domain Controllers by scanning for open port 88.

---

## DNS

Active Directory Domain Services (AD DS) relies on DNS to enable clients to locate Domain Controllers and for Domain Controllers to communicate with each other. DNS resolves hostnames to IP addresses and is critical for AD environments.

### Key Points:
- **Service Records (SRV)**: Used to locate services in the network, like file servers or Domain Controllers.
- **Dynamic DNS**: Allows automatic updates when an IP address changes, reducing manual work and errors.
- **DNS Protocol**: Uses **TCP/UDP port 53** (default UDP, falls back to TCP for larger messages).

When a client joins the network, it queries DNS for the Domain Controller's SRV record, retrieves the hostname, and then resolves it to an IP address.

---

## LDAP

Active Directory supports **Lightweight Directory Access Protocol (LDAP)** for directory lookups. LDAP is open-source and cross-platform, allowing communication between various directory services like AD.

### Key Points:
- **Port 389** (LDAP) and **Port 636** (LDAPS).
- **BIND** operation is used for authentication in LDAP, where a username/password or SASL authentication (e.g., Kerberos) binds to the LDAP server.
- **LDAP** allows querying AD for user information, passwords, etc.

#### Types of LDAP Authentication:
1. **Simple Authentication**: Includes anonymous authentication and username/password authentication.
2. **SASL Authentication**: Uses external authentication methods like Kerberos.

LDAP authentication is often transmitted in **cleartext**, so using **TLS encryption** is recommended.

---

## MSRPC (Microsoft RPC)

MSRPC is Microsoft's implementation of **Remote Procedure Call (RPC)**, used for client-server communication in Active Directory environments.

### Key MSRPC Interfaces:

| Interface Name | Description |
|----------------|-------------|
| **lsarpc** | Manages local security policy, audit policy, and authentication. |
| **netlogon** | Authenticates users and services in the domain environment. |
| **samr** | Provides management functions for domain account databases (users, groups, etc.). |
| **drsuapi** | Used for directory replication across Domain Controllers. |

### Reconnaissance Using MSRPC:
- **Samr Protocol**: Attackers can query the **SAM** to gather information about users and groups.
- **drsuapi Protocol**: Attackers can replicate the AD domain database (**NTDS.dit**) to extract password hashes for Pass-the-Hash attacks.

### Protection Measures:
- Restrict **remote SAM queries** to administrators to prevent unauthorized reconnaissance.
- Use **TLS encryption** to protect MSRPC communications.

---

### Summary:
- **Kerberos** is a stateless, ticket-based authentication protocol used in AD.
- **DNS** facilitates Domain Controller discovery and communication in an AD environment.
- **LDAP** is used for directory lookups and can authenticate against AD.
- **MSRPC** allows client-server communication in AD, with key interfaces for authentication and directory replication.
