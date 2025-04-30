---
title: 13-8-User & Machine Accounts 
seriesId: 13-Active-Directory
publishDate: "2025-04-29T15:12:00Z"
---

# User and Machine Accounts

User accounts are created on both local systems (not joined to AD) and in Active Directory to give a person or a program (such as a system service) the ability to log on to a computer and access resources based on their rights. When a user logs in, the system verifies their password and creates an access token. This token describes the security content of a process or thread and includes the user's security identity and group membership. Whenever a user interacts with a process, this token is presented. 

User accounts are used to:
- Allow employees/contractors to log in to a computer and access resources.
- Run programs or services under a specific security context (i.e., running as a highly privileged user instead of a network service account).
- Manage access to objects and their properties, such as network file shares, files, and applications.

Users can be assigned to groups that can contain one or more members. These groups can also be used to control access to resources. It can be easier for an administrator to assign privileges once to a group (which all group members inherit) instead of many times to each individual user. This simplifies administration and makes it easier to grant and revoke user rights.

The ability to provision and manage user accounts is one of the core elements of Active Directory. Typically, every company will have at least one AD user account provisioned per user. Some users may have two or more accounts based on their job role (e.g., IT admins or Help Desk members). Additionally, many service accounts are used to run applications or services in the background.

In larger organizations, the number of active user accounts may exceed the number of employees, and it is common to find hundreds of disabled accounts from former employees, temporary workers, and interns. These accounts are typically deactivated but not deleted for audit purposes, often stored in Organizational Units (OUs) like **FORMER EMPLOYEES**.

User accounts can be provisioned with varying rights, from basic read-only access to complete control as an **Enterprise Admin**. Misconfigurations in user accounts can lead to unintended privileges, which attackers can leverage. Users are often the weakest link in any organization, making user accounts a key target in penetration tests.

### Local Accounts

Local accounts are stored locally on a server or workstation and can only manage resources on that specific machine. They do not work across the domain.

#### Default Local Accounts:
- **Administrator**: SID `S-1-5-domain-500`, first account created during a Windows installation. Full control over most system resources, but it can be disabled or renamed (though it can't be deleted).
- **Guest**: Disabled by default. Used for temporary access by users without an account. Typically recommended to stay disabled due to security risks.
- **SYSTEM**: Also known as `NT AUTHORITY\SYSTEM`. The highest permission level on a Windows host. It doesn’t have a profile, but it controls almost everything on the system.
- **Network Service**: A predefined local account used by the Service Control Manager (SCM) to run services. Presents credentials to remote services when needed.
- **Local Service**: Another predefined account used by the SCM for running services. Configured with minimal privileges and presents anonymous credentials.

It is essential to understand how these local accounts interact within the system, especially for security purposes.

### Domain Users

Domain users are granted rights from the domain to access resources like file servers, printers, intranet hosts, etc., based on permissions. Unlike local users, domain users can log in to any host within the domain.

One important account to consider is the **KRBTGT** account, which acts as a service account for the Key Distribution Service. This account is a frequent target for attackers because gaining control can lead to full access to the domain.

### User Naming Attributes

To improve security, Active Directory uses specific naming attributes to identify user objects:
- **UserPrincipalName (UPN)**: The primary logon name, typically using the user’s email address.
- **ObjectGUID**: A unique identifier for the user that remains unchanged even if the user is deleted.
- **SAMAccountName**: A legacy logon name for older versions of Windows.
- **objectSID**: The user’s Security Identifier, which identifies the user and group memberships.
- **sIDHistory**: Contains previous SIDs if the user was moved from another domain, typically used in migration scenarios.

### Domain-joined vs. Non-Domain-joined Machines

#### Domain-joined
Hosts joined to a domain have centralized management and access to resources through domain policies. Users can log in from any domain-joined host, not just the one they are physically working on. This is common in enterprise environments.

#### Non-domain-joined
These machines are not managed by domain policies. Sharing resources outside the local network is much more complex, making this setup suitable for small businesses or home networks. User accounts exist only on that host, and profiles are not migrated across machines.

### Machine Accounts

Machine accounts in an AD environment, such as `NT AUTHORITY\SYSTEM`, are granted rights similar to standard domain user accounts. Gaining access to a system as the SYSTEM account can be a crucial step in enumerating and attacking a domain. SYSTEM-level access on a domain-joined machine can be leveraged for privilege escalation and obtaining critical information within the domain.

---

This summary outlines the importance of user and machine accounts in an Active Directory environment. Understanding the roles and configurations of these accounts helps in managing user access and securing a domain network.
