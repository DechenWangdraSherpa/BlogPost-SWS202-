---
title: 3-7-Subdomain BruteForcing
seriesId: 3-Web-Information-Gathering
publishDate: "2025-04-22T15:00:00Z"
---

# Subdomain Bruteforcing

Subdomain Bruteforce Enumeration is a popular and effective active technique used to discover subdomains by testing a predefined list of potential names. This method can be crucial for uncovering hidden or forgotten subdomains that could expose sensitive information or vulnerabilities.

## Steps in Subdomain Bruteforcing

### 1. Wordlist Selection
Wordlists are at the core of this technique. These lists contain potential subdomain names that are tested against the target domain. Wordlists can be:
- **General-Purpose**: A broad set of common subdomains such as `dev`, `staging`, `blog`, `mail`, `admin`, and `test`. These are useful when you don’t know the target’s specific naming conventions.
- **Targeted**: Lists tailored to the target’s industry or known technologies, improving the efficiency of the scan and reducing false positives.
- **Custom**: Custom-built lists based on intelligence gathered from other sources or specific keywords related to the target.

### 2. Iteration and Querying
Once a wordlist is selected, a script or tool iterates over each word, appending it to the main domain. For example, if the domain is `example.com`, it would test potential subdomains like `dev.example.com`, `staging.example.com`, etc.

### 3. DNS Lookup
For each subdomain, a DNS query is performed (usually an A or AAAA record query) to check if the subdomain resolves to an IP address. A valid response indicates the subdomain exists.

### 4. Filtering and Validation
After querying, any subdomains that resolve successfully are added to a list of valid subdomains. Further validation may be done to confirm their functionality, such as attempting to access them through a browser.

## Tools for Subdomain Bruteforcing

| Tool         | Description                                                                 |
|--------------|-----------------------------------------------------------------------------|
| **dnsenum**  | A comprehensive DNS enumeration tool that supports both brute-force and dictionary-based subdomain discovery. It can attempt zone transfers, perform reverse lookups, and scrape Google results for additional subdomains. |
| **fierce**   | Known for its user-friendly interface, fierce is another popular tool for subdomain discovery. It features recursive search and wildcard detection, making it a great option for DNS reconnaissance. |
| **dnsrecon** | This tool combines several DNS reconnaissance techniques and allows customizable output formats, making it a versatile choice for DNS enumeration. |
| **amass**    | Actively maintained and focused on subdomain discovery, amass integrates with various data sources and offers extensive options for subdomain enumeration. |
| **assetfinder** | A quick and effective tool for discovering subdomains, assetfinder is ideal for lightweight scans. |
| **puredns**  | A robust tool for DNS brute-forcing, puredns is capable of filtering and resolving DNS queries efficiently. |

## Using **dnsenum** for Subdomain Bruteforcing

`dnsenum` is a powerful tool that can be used for comprehensive DNS reconnaissance. Let's demonstrate how to use `dnsenum` for subdomain bruteforce enumeration.

Here’s an example of how to run `dnsenum` with the `subdomains-top1million-5000.txt` wordlist from SecLists, which contains the top 5000 most common subdomains:

```bash
dnsenum --enum --dnsserver 8.8.8.8 --subdomains --wordlist=/path/to/subdomains-top1million-5000.txt inlanefreight.com
