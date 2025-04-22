---
title: 3-2-WHOIS
seriesId: 3-Web-Information-Gathering
publishDate: "2025-04-22T13:30:00Z"
---

## WHOIS

WHOIS is a standard protocol used to query databases that store information about registered internet resources. Most commonly associated with domain names, WHOIS can also be used to retrieve details about IP address blocks and autonomous systems. Think of WHOIS as the internet's version of a phonebook—it tells you who owns or manages various online assets.

### What Information Does WHOIS Provide?

A typical WHOIS record includes:

- **Domain Name**: The fully qualified domain name (e.g., `example.com`).
- **Registrar**: The company where the domain was registered, such as GoDaddy or Namecheap.
- **Registrant Contact**: The person or organization that owns the domain.
- **Administrative Contact**: The person responsible for managing the domain.
- **Technical Contact**: The contact for technical issues related to the domain.
- **Creation and Expiration Dates**: When the domain was registered and when it will expire.
- **Name Servers**: DNS servers that resolve the domain to its IP address.

---

### A Brief History of WHOIS

The origins of WHOIS trace back to the 1970s, when Elizabeth Feinler and her team at the Network Information Center (NIC) at Stanford Research Institute saw the need for a central system to track resources on the ARPANET—an early version of the internet. Their solution was the WHOIS directory, a pioneering database that cataloged network users, hostnames, and domain names. Over time, this system evolved into the global WHOIS service we use today.

---

### Why WHOIS is Important in Web Recon

WHOIS data is incredibly valuable during the reconnaissance phase of a penetration test. It reveals key insights into a target's digital footprint and can even uncover potential weaknesses:

- **Identifying Key Personnel**: WHOIS entries often list names, emails, and phone numbers of individuals who manage the domain. This information is useful for crafting targeted social engineering or phishing attacks.
- **Understanding Network Infrastructure**: Technical information like name servers and associated IPs can expose details about how a company’s network is structured, possibly revealing misconfigurations or overlooked services.
- **Historical WHOIS Data**: By examining past WHOIS records using tools like WhoisFreaks, testers can track how a domain’s ownership or configuration has changed over time. This might reveal older, forgotten infrastructure that is still exposed.

---

WHOIS remains one of the most basic yet powerful tools in a penetration tester’s toolkit. It’s a starting point for mapping out a target and laying the groundwork for deeper investigation.
