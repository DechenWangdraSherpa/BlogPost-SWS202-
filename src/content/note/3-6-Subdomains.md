---
title: 3-6-Subdomains
seriesId: 3-Web-Information-Gathering
publishDate: "2025-04-22T14:40:00Z"
---

## Subdomains in Web Reconnaissance

When analyzing DNS records, we often focus on the primary domain (e.g., `example.com`). However, subdomains are equally important as they often represent separate services, applications, or environments under the same root domain.

###  What Are Subdomains?

Subdomains are prefixes to the main domain name, used to organize content or services. For example:

- `blog.example.com` – company blog  
- `shop.example.com` – online store  
- `mail.example.com` – email services

---

###  Why Subdomains Matter in Reconnaissance

Subdomains can reveal:

- **Development & Staging Environments**  
  Often less secure and may contain vulnerabilities or unfinished features.

- **Hidden Login Portals**  
  Admin panels or other login pages not linked from the main site.

- **Legacy Applications**  
  Outdated systems that may have known exploits.

- **Sensitive Information**  
  Misconfigured subdomains might expose private documents, configs, or internal dashboards.

---

##  Subdomain Enumeration

Subdomain enumeration is the process of discovering subdomains associated with a target domain. Subdomains typically appear as `A` or `AAAA` DNS records (IPv4/IPv6), or as `CNAME` aliases.

---

###  1. Active Subdomain Enumeration

**Definition**: Directly querying the domain’s DNS servers to discover subdomains.

####  Techniques

- **DNS Zone Transfer**:  
  Attempts to retrieve the entire DNS zone from misconfigured servers.  
  _Rarely successful due to modern DNS security settings._

- **Brute-Force Enumeration**:  
  Tries common or custom subdomain names using a wordlist.  
  **Tools**:
  - `dnsenum`
  - `ffuf`
  - `gobuster`

####  Pros
- Detailed and controllable  
- High discovery rate with the right wordlists

####  Cons
- More detectable  
- Can be rate-limited or blocked

---

###  2. Passive Subdomain Enumeration

**Definition**: Uses external data sources to discover subdomains without contacting the target's infrastructure.

####  Techniques

- **Certificate Transparency (CT) Logs**  
  - TLS/SSL certificates often list subdomains in their SAN (Subject Alternative Name) field.

- **Search Engine Operators**  
  - Example: `site:*.example.com`  
  - Works on Google, DuckDuckGo, etc.

- **Public Databases and OSINT Tools**  
  - Tools like `theHarvester`  
  - Online services: `crt.sh`, `Shodan`, `Censys`, `SecurityTrails`, `VirusTotal`

####  Pros
- Stealthy and undetectable  
- No interaction with target’s servers

####  Cons
- May miss unindexed or internal subdomains  
- Dependent on third-party data freshness

---

###  Recommended Strategy

**Combine Active + Passive Enumeration**:
- Passive for stealth and broad overview
- Active for deeper, controlled probing

This hybrid approach maximizes discovery while minimizing detection risk.
