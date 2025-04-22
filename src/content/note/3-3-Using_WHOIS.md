---
title: 3-3-Using WHOIS
seriesId: 3-Web-Information-Gathering
publishDate: "2025-04-22T13:50:00Z"
---

## Utilising WHOIS

WHOIS data can offer crucial insights when investigating suspicious activities, analyzing threats, or compiling threat intelligence. Below are three scenarios that demonstrate how WHOIS is used effectively during reconnaissance and investigation.

---

### Scenario 1: Phishing Investigation

A company receives a suspicious email that appears to come from its bank, urging employees to click a link and update account details. A security analyst investigates by performing a WHOIS lookup on the domain in the email.

**WHOIS Findings:**

- **Registration Date**: The domain was registered just a few days ago.
- **Registrant**: The information is hidden behind a privacy protection service.
- **Name Servers**: Associated with a known bulletproof hosting provider.

**Conclusion**:  
These indicators raise significant concerns. The analyst reports the findings, blocks the domain, and warns employees. Additional investigation into related infrastructure could uncover more phishing domains.

---

### Scenario 2: Malware Analysis

A security researcher is analyzing malware that communicates with a command-and-control (C2) server. The researcher performs a WHOIS lookup on the server’s domain.

**WHOIS Findings:**

- **Registrant**: Uses a free, anonymizing email service.
- **Location**: Based in a country with high cybercrime activity.
- **Registrar**: Known for poor abuse management.

**Conclusion**:  
The C2 domain is likely hosted on a bulletproof server. The researcher contacts the hosting provider and continues mapping out the infrastructure using WHOIS and other tools.

---

### Scenario 3: Threat Intelligence Report

A cybersecurity firm monitors a known threat group targeting financial institutions. Analysts compile WHOIS data from domains used in past campaigns.

**Observed Patterns:**

- **Registration Dates**: Domains registered in clusters, just before attacks.
- **Registrant Info**: Uses fake names or aliases.
- **Name Servers**: Shared across multiple campaigns.
- **Takedown Records**: Domains often deactivated after use.

**Outcome**:  
Analysts develop a detailed TTP (Tactics, Techniques, and Procedures) profile. The report includes IOCs (Indicators of Compromise) derived from WHOIS data to aid others in threat detection.

---

## Using the WHOIS Command

To use the `whois` tool, ensure it's installed:

```bash
sudo apt install whois

