---
title: 2-9-DNS
seriesId: 2-Footprinting
publishDate: "2025-04-22T01:30:00Z"
---

# DNS (Domain Name System)

## Overview
The Domain Name System (DNS) is an essential part of the Internet. It resolves domain names like `academy.hackthebox.com` or `www.hackthebox.com` into IP addresses, enabling users to reach web servers. DNS operates as a decentralized system without a central database, with information distributed across thousands of name servers worldwide.

## Types of DNS Servers

| Server Type               | Description |
|---------------------------|-------------|
| **DNS Root Server**        | Responsible for the top-level domains (TLDs). They link domains to IP addresses and are a central interface between users and content on the Internet. There are 13 root servers worldwide. |
| **Authoritative Nameserver** | Holds authority for a specific zone. Only answers queries for its designated zone. If it can't answer, the query is passed to a root server. |
| **Non-authoritative Nameserver** | Does not hold authority for a zone. Instead, it queries other servers recursively or iteratively to collect DNS information. |
| **Caching DNS Server**     | Caches DNS data from authoritative name servers for a specified time. The duration of this cache is determined by the authoritative server. |
| **Forwarding Server**      | Forwards DNS queries to other DNS servers, typically used in specific configurations where queries are directed to a central DNS server. |
| **Resolver**               | Resolves domain names locally on the client or router. Not authoritative but plays a role in resolving queries for clients. |

## DNS Security
- **Unencrypted by Default**: DNS traffic is typically unencrypted, making it vulnerable to interception and eavesdropping by local networks or Internet providers.
- **DNS Encryption Solutions**: To address privacy concerns, solutions like **DNS over TLS (DoT)**, **DNS over HTTPS (DoH)**, and **DNSCrypt** are used to encrypt DNS queries between clients and servers.

## DNS Records
DNS queries use various record types to return different kinds of information about a domain. Some common DNS record types are:

| DNS Record Type | Description |
|-----------------|-------------|
| **A**           | Returns the IPv4 address of the requested domain. |
| **AAAA**        | Returns the IPv6 address of the requested domain. |
| **MX**          | Returns the mail servers responsible for the domain. |
| **NS**          | Returns the nameservers of the domain. |
| **TXT**         | Can contain arbitrary text, often used for validation (e.g., Google Search Console, SSL certificates) or email security (SPF, DMARC). |
| **CNAME**       | An alias for another domain name. E.g., `www.hackthebox.eu` pointing to `hackthebox.eu`. |
| **PTR**         | Performs a reverse lookup, converting IP addresses into valid domain names. |
| **SOA**         | Specifies the start of a DNS zone, containing information about the domain’s administration and management. |

## Summary
- **Decentralized System**: DNS is a distributed system with no central database, allowing efficient resolution of domain names to IP addresses globally.
- **Multiple Server Types**: Various DNS servers (root, authoritative, caching, etc.) work together to resolve queries.
- **Security Enhancements**: DNS encryption (DoT, DoH, DNSCrypt) helps address privacy concerns by protecting DNS traffic.
- **DNS Records**: Different record types are used to store and retrieve information like IP addresses, mail servers, aliases, and more.
