---
title: 2-3-Domain Information
seriesId: 2-Footprinting
publishDate: "2025-04-21T21:20:55Z"
---

# Domain Information Gathering Walkthrough (Passive OSINT)

## Objective
To collect valuable information about a target domain using passive reconnaissance techniques. This helps identify publicly available data without directly interacting with the target systems.

---
## 1. Understanding Passive Reconnaissance
- Passive reconnaissance involves collecting data from third-party sources without alerting the target.
- No direct interaction with the target’s infrastructure.
- Useful for staying undetected and gathering early intel.

---

## 2. Target Domain Example
- Target domain: `example.com`

---

## 3. SSL Certificate Analysis using crt.sh
- **Tool:** [crt.sh](https://crt.sh/)
- **Purpose:** View SSL certificates issued to a domain.
- **Process:**
  - Go to `https://crt.sh/`
  - Search for `%.example.com` to see all subdomains listed in SSL certificates.
- **Benefits:**
  - Discover subdomains that may not be indexed by search engines.
  - Reveal internal services (e.g., `dev.example.com`, `vpn.example.com`).
  - Get timestamps of when certs were issued or renewed.

---

## 4. DNS Records Lookup using dig
- **Tool:** `dig` (command-line tool)
- **Purpose:** Retrieve domain's DNS records.
- **Commands:**
  - `dig example.com` → Get A (IPv4) records.
  - `dig example.com MX` → Get mail servers.
  - `dig example.com NS` → List name servers.
  - `dig example.com TXT` → View text records (often contain SPF/DKIM info).
- **Tips:**
  - Can also run `dig any example.com` to get all available record types.
- **Outcome:** Identifies IPs, servers, and services used by the domain.

---

## 5. Subdomain Enumeration using crt.sh and dig
- Combine `crt.sh` output with `dig` to validate and resolve discovered subdomains.
- Confirm which subdomains are alive or point to active IPs.

---

## 6. Infrastructure Discovery with Shodan
- **Tool:** [Shodan](https://www.shodan.io/)
- **Purpose:** Find internet-facing systems and services.
- **Steps:**
  - Search for `hostname:example.com` or `ssl.cert.subject.CN:"example.com"`
  - Review open ports, banner info, service versions.
  - Look for IoT devices, webcams, servers, APIs, VPNs.
- **Outcome:** Understand what systems are publicly accessible.

---

## 7. WHOIS Lookup
- **Tool:** `whois` (or web services like who.is)
- **Purpose:** Gather domain registration details.
- **Findings:**
  - Registrar, registration date, expiration date.
  - Sometimes includes contact info (if not protected by privacy services).
- **Use Case:** Helps trace domain ownership and infrastructure timeline.

---

## 8. Reverse IP Lookup
- **Tools:** `viewdns.info`, `securitytrails.com`, `censys.io`
- **Purpose:** Find other domains hosted on the same server.
- **Benefit:** Reveal sister sites or staging environments.

---

## 9. Search Engine Dorking (Google Hacking)
- **Example Queries:**
  - `site:example.com` → All indexed pages.
  - `site:example.com filetype:pdf` → Find publicly available files.
  - `"confidential" site:example.com` → Look for sensitive content.
- **Use Case:** Find exposed documents, login pages, backups.

---

## Summary of Key Tools

| Tool        | Purpose                                  |
|-------------|------------------------------------------|
| `crt.sh`    | Find SSL certificate and subdomains      |
| `dig`       | Extract DNS records                      |
| `Shodan`    | Identify open ports and devices          |
| `whois`     | Domain registration and ownership info   |
| `Google`    | Publicly indexed data via search dorking |
| `viewdns`   | Reverse IP for hosted domains            |
