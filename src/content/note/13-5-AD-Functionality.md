---
title: 13-4-AD Functionality 
seriesId: 13-Active-Directory
publishDate: "2025-04-29T14:35:00Z"
---

# Active Directory: Functionality

## FSMO Roles (Flexible Single Master Operation)

| Role                  | Description |
|-----------------------|-------------|
| **Schema Master**     | Manages the read/write copy of the AD schema. Defines all object attributes in AD. |
| **Domain Naming Master** | Ensures domain names are unique within a forest. Manages additions of new domains. |
| **Relative ID (RID) Master** | Assigns RID blocks to other DCs. Helps form unique SIDs by combining domain SID + RID. |
| **PDC Emulator**      | Authoritative DC for time, password changes, Group Policy, and authentication. |
| **Infrastructure Master** | Resolves SIDs/GUIDs/DNs across domains for ACL readability in multi-domain forests. |

> Issues with FSMO roles can cause authentication and authorization failures.

---

## Domain & Forest Functional Levels

Functional levels determine the features available and compatible Domain Controller (DC) OS versions.

### Domain Functional Levels

| Domain Functional Level | Features | Supported DC OS |
|-------------------------|----------|------------------|
| **Windows 2000 native** | Universal groups, group nesting, SID history | Windows Server 2008 R2 → 2000 |
| **Windows Server 2003** | `lastLogonTimestamp`, constrained delegation, netdom, selective authentication | WS 2012 R2 → 2003 |
| **Windows Server 2008** | DFS-R support, Kerberos AES support, Fine-grained password policies | WS 2012 R2 → 2008 |
| **Windows Server 2008 R2** | Auth mechanism assurance, Managed Service Accounts | WS 2012 R2, 2012, 2008 R2 |
| **Windows Server 2012** | KDC support for claims, compound auth, Kerberos armoring | WS 2012 R2, 2012 |
| **Windows Server 2012 R2** | Protected Users, Auth Policies, Policy Silos | WS 2012 R2 |
| **Windows Server 2016** | Smart card-only login, new Kerberos and credential protection features | WS 2019, 2016 |

> **Note**: No new functional level for Windows Server 2019.  
> **Minimum requirement** for adding Server 2019 DC: **Windows Server 2008 functional level** and **DFS-R for SYSVOL**.

---

### Forest Functional Levels

| Version                  | Key Capabilities |
|--------------------------|------------------|
| **Windows Server 2003**  | Forest trusts, domain renaming, RODC |
| **Windows Server 2008**  | No new features; new domains default to 2008 level |
| **Windows Server 2008 R2** | AD Recycle Bin (restore deleted objects) |
| **Windows Server 2012**  | No new features; new domains default to 2012 |
| **Windows Server 2012 R2** | No new features; new domains default to 2012 R2 |
| **Windows Server 2016**  | PAM (Privileged Access Management) using MIM |

---

## Trusts in Active Directory

Used to enable cross-domain or cross-forest authentication and resource access.

### Types of Trusts

| Type         | Description |
|--------------|-------------|
| **Parent-child** | Two-way transitive trust between a parent domain and its child. |
| **Cross-link**   | Trust between child domains to improve authentication performance. |
| **External**     | Non-transitive trust between domains in separate forests. Uses SID filtering. |
| **Tree-root**    | Two-way transitive trust between the forest root and a new tree root domain. |
| **Forest**       | Transitive trust between two forest root domains. |

### Trusts can be:
 - **Transitive**: Trust is extended to other trusted domains.
 - **Non-transitive**: Trust is limited to the specified domains only.
 - **One-way**: Only users from the trusted domain can access the trusting domain.
 - **Two-way (bidirectional)**: Users from both domains can access each other's resources.
### **Security Note**:
 - Misconfigured trusts are a common source of vulnerabilities.
 - Bidirectional trusts, often set up during mergers, can enable attacks like **Kerberoasting** across domains.