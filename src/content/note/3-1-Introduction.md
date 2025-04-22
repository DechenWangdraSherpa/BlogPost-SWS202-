---
title: 3-1-Introduction To Web Reconnaissance
seriesId: 3-Web-Information-Gathering
publishDate: "2025-04-22T13:10:00Z"
---

# Web Reconnaissance

Web reconnaissance is a crucial step in any security assessment. It's the phase where we systematically collect information about a target website or web application. Think of it as laying the groundwork before diving into more detailed analysis or attempting exploitation. This phase is part of the broader "Information Gathering" process in penetration testing.

## Why is Web Recon Important?

The goal of web reconnaissance is to build a complete picture of the target. This includes:

- **Identifying Assets**: Discovering all public-facing elements like web pages, subdomains, IP addresses, and technologies. This forms the baseline of what the target has exposed online.
- **Uncovering Hidden Information**: Finding potentially sensitive or forgotten files—like backups, config files, or internal documentation—that could leak valuable intel.
- **Analyzing the Attack Surface**: Understanding how the site is built, what technologies are used, and where weak points might be. This helps in planning potential exploitation paths.
- **Gathering Intelligence**: Collecting data about employees, email addresses, or usage patterns that might be useful in crafting social engineering attacks.

Recon is used by attackers to identify weaknesses and tailor their attacks accordingly. At the same time, defenders can use it to spot and fix issues before they’re exploited.

## Types of Web Reconnaissance

Reconnaissance can be divided into two main approaches:

---

### Active Reconnaissance

Active recon involves directly interacting with the target system to pull information. While this method can yield in-depth results, it also increases the risk of being detected.

| Technique            | Description                                                                 | Example                                                   | Tools                        | Detection Risk        |
|----------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------|-------------------------------|------------------------|
| Port Scanning        | Finds open ports and services.                                              | Scanning for HTTP (80) and HTTPS (443) ports.            | Nmap, Masscan, Unicornscan   | **High**              |
| Vulnerability Scanning | Checks for known vulnerabilities like outdated software or bad configs.     | Using Nessus to detect SQLi or XSS.                      | Nessus, OpenVAS, Nikto        | **High**              |
| Network Mapping      | Reveals network structure and device relationships.                         | Using `traceroute` to track packet path.                 | Traceroute, Nmap              | **Medium to High**    |
| Banner Grabbing      | Reads banners from services to gather software and version info.            | Curling port 80 to read HTTP response header.            | Netcat, curl                  | **Low**               |
| OS Fingerprinting    | Identifies the operating system of the target machine.                      | Using `nmap -O` to detect OS.                            | Nmap, Xprobe2                 | **Low**               |
| Service Enumeration  | Determines exact versions of running services.                              | Using `nmap -sV` for version detection.                  | Nmap                          | **Low**               |
| Web Spidering        | Crawls the website to find hidden files and folders.                        | Using Burp Suite Spider to map the site.                 | Burp Spider, ZAP, Scrapy      | **Low to Medium**     |

---

### Passive Reconnaissance

Passive recon gathers data without ever touching the target system. It’s stealthy, but can be limited to only what’s publicly available.

| Technique            | Description                                                                 | Example                                                   | Tools                        | Detection Risk        |
|----------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------|-------------------------------|------------------------|
| Search Engine Queries| Uses Google or other engines to find related data.                          | Googling "[Target Name] employees".                      | Google, DuckDuckGo, Shodan    | **Very Low**          |
| WHOIS Lookups        | Retrieves domain registration and ownership info.                           | WHOIS lookup on a domain to get contact details.         | `whois`, online tools         | **Very Low**          |
| DNS Analysis         | Checks DNS records for subdomains and mail servers.                         | Using `dig` to find subdomains.                          | dig, dnsenum, dnsrecon        | **Very Low**          |
| Web Archive Analysis | Views older versions of the target’s website.                               | Using Wayback Machine to inspect past content.           | Wayback Machine               | **Very Low**          |
| Social Media Analysis| Collects information from public social media profiles.                     | Finding employee data via LinkedIn.                      | LinkedIn, Twitter             | **Very Low**          |
| Code Repositories    | Examines public repos for leaks like API keys or secrets.                   | Searching GitHub for target-related code.                | GitHub, GitLab                | **Very Low**          |

---

In this module, we’ll start by exploring WHOIS—an essential protocol for retrieving domain ownership and registration info. Understanding WHOIS is a critical first step in mastering web recon, as it lays the groundwork for deeper exploration of a target's infrastructure.
