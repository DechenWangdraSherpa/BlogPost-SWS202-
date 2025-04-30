---
title: 13-2-AD Structure
seriesId: 13-Active-Directory
publishDate: "2025-04-29T13:30:00Z"
---

# Active Directory Structure

Active Directory (AD) is a directory service developed by Microsoft for managing Windows network environments. It is built upon a **distributed, hierarchical structure** and enables centralized management of an organization’s digital resources. These resources include **users, computers, groups, network devices, file shares, group policies, servers, workstations, and trusts**.

## Purpose and Role of AD

AD provides **authentication** and **authorization** within a Windows domain. A component called **Active Directory Domain Services (AD DS)** handles this by storing and organizing information such as **usernames, passwords, and user access rights**. Both administrators and standard users can access this data depending on their permissions. First introduced with **Windows Server 2000**, AD has remained a core part of enterprise infrastructure and has been a frequent target for attackers due to its critical role.

### Key Characteristics

- **Backward-Compatible:** Designed to support legacy systems, though many default settings are not secure.
- **Misconfiguration-Prone:** Particularly in large environments, improper setup or lack of hardening can lead to serious vulnerabilities.
- **Accessible to All Users:** Even standard domain users can **enumerate** (i.e., query and discover) most objects in the AD environment.

## Objects Enumerated by Any AD User

Even a low-privileged user can typically view:

- Domain Computers  
- Domain Users  
- Domain Group Information  
- Organizational Units (OUs)  
- Default Domain Policy  
- Functional Domain Levels  
- Password Policy  
- Group Policy Objects (GPOs)  
- Domain Trusts  
- Access Control Lists (ACLs)

Understanding these objects is critical before attempting penetration testing. One must understand how AD is **built and managed** in order to exploit it effectively.

---

## Hierarchical Structure

Active Directory is arranged in a **tree structure**, with a **forest** at the top level. This forest contains one or more **domains**, which can themselves have **nested subdomains**. Each level has distinct administrative and security functions.

### Terminology

- **Forest:** The top-level container and security boundary. It can contain multiple domains.
- **Domain:** A logical grouping of users, computers, and resources. Domains can be **parents or children** to other domains.
- **Organizational Units (OUs):** Containers within domains used to organize users, computers, and groups. OUs can also contain other sub-OUs and have **Group Policy Objects (GPOs)** applied to them.

### Active Directory Structure

```bash
INLANEFREIGHT.LOCAL/
├── ADMIN.INLANEFREIGHT.LOCAL
│ ├── GPOs
│ └── OU
│ └── EMPLOYEES
│ ├── COMPUTERS
│ │ └── FILE01
│ ├── GROUPS
│ │ └── HQ Staff
│ └── USERS
│ └── barbara.jones
├── CORP.INLANEFREIGHT.LOCAL
└── DEV.INLANEFREIGHT.LOCAL
```


In this layout:

- `INLANEFREIGHT.LOCAL` is the **root domain**.
- `ADMIN`, `CORP`, and `DEV` are **subdomains** under the root.
- OUs such as `EMPLOYEES` organize users and computers and can have custom GPOs applied to them.

---

## Trust Relationships

In large enterprises, multiple forests may exist due to mergers or departmental boundaries. Instead of migrating every object, **trust relationships** are established between forests or domains.

### Example: Cross-Forest Trust

``INLANEFREIGHT.LOCAL <---- Bidirectional Trust ----> FREIGHTLOGISTICS.LOCAL``

- This bidirectional trust allows users from one forest to access resources in another.
- **Child domains** under each root domain do **not automatically** inherit trust with child domains from another forest.
- For example, a user from `admin.dev.freightlogistics.local` **cannot access** `wh.corp.inlanefreight.local` unless an **additional trust** is set up.

### Key Point

- Trusts can greatly **increase complexity** and introduce potential **security risks** if not configured correctly.

---