---
title: 13-10-AD Rights and Privileges
seriesId: 13-Active-Directory
publishDate: "2025-04-30T15:30:00Z"
---

# Active Directory Rights and Privileges

Rights and privileges are the cornerstones of AD management and, if mismanaged, can easily lead to abuse by attackers or penetration testers.  
Access rights and privileges are two important topics in AD (and infosec in general), and we must understand the difference. Rights are typically assigned to users or groups and deal with permissions to access an object such as a file, while privileges grant a user permission to perform an action such as run a program, shut down a system, reset passwords, etc. Privileges can be assigned individually to users or conferred upon them via built-in or custom group membership.  

Windows computers have a concept called User Rights Assignment, which, while referred to as rights, are actually types of privileges granted to a user. We will discuss these later in this section. We must have a firm grasp of the differences between rights and privileges in a broader sense and precisely how they apply to an AD environment.

## Built-in AD Groups

AD contains many default or built-in security groups, some of which grant their members powerful rights and privileges which can be abused to escalate privileges within a domain and ultimately gain Domain Admin or SYSTEM privileges on a Domain Controller (DC). Membership in many of these groups should be tightly managed as excessive group membership/privileges is a common flaw in many AD networks that attackers look to abuse. Some of the most common built-in groups are listed below.

| Group Name | Description |
|------------|-------------|
| **Account Operators** | Members can create and modify most types of accounts, including those of users, local groups, and global groups, and members can log in locally to domain controllers. They cannot manage the Administrator account, administrative user accounts, or members of the Administrators, Server Operators, Account Operators, Backup Operators, or Print Operators groups. |
| **Administrators** | Members have full and unrestricted access to a computer or an entire domain if they are in this group on a Domain Controller. |
| **Backup Operators** | Members can back up and restore all files on a computer, regardless of the permissions set on the files. Backup Operators can also log on to and shut down the computer. Members can log onto DCs locally and should be considered Domain Admins. They can make shadow copies of the SAM/NTDS database, which, if taken, can be used to extract credentials and other juicy info. |
| **DnsAdmins** | Members have access to network DNS information. The group will only be created if the DNS server role is or was at one time installed on a domain controller in the domain. |
| **Domain Admins** | Members have full access to administer the domain and are members of the local administrator's group on all domain-joined machines. |
| **Domain Computers** | Any computers created in the domain (aside from domain controllers) are added to this group. |
| **Domain Controllers** | Contains all DCs within a domain. New DCs are added to this group automatically. |
| **Domain Guests** | This group includes the domain's built-in Guest account. Members of this group have a domain profile created when signing onto a domain-joined computer as a local guest. |
| **Domain Users** | This group contains all user accounts in a domain. A new user account created in the domain is automatically added to this group. |
| **Enterprise Admins** | Membership in this group provides complete configuration access within the domain. The group only exists in the root domain of an AD forest. Members in this group are granted the ability to make forest-wide changes such as adding a child domain or creating a trust. The Administrator account for the forest root domain is the only member of this group by default. |
| **Event Log Readers** | Members can read event logs on local computers. The group is only created when a host is promoted to a domain controller. |
| **Group Policy Creator Owners** | Members create, edit, or delete Group Policy Objects in the domain. |
| **Hyper-V Administrators** | Members have complete and unrestricted access to all the features in Hyper-V. If there are virtual DCs in the domain, any virtualization admins, such as members of Hyper-V Administrators, should be considered Domain Admins. |
| **IIS_IUSRS** | This is a built-in group used by Internet Information Services (IIS), beginning with IIS 7.0. |
| **Pre–Windows 2000 Compatible Access** | This group exists for backward compatibility for computers running Windows NT 4.0 and earlier. Membership in this group is often a leftover legacy configuration. It can lead to flaws where anyone on the network can read information from AD without requiring a valid AD username and password. |
| **Print Operators** | Members can manage, create, share, and delete printers that are connected to domain controllers in the domain along with any printer objects in AD. Members are allowed to log on to DCs locally and may be used to load a malicious printer driver and escalate privileges within the domain. |
| **Protected Users** | Members of this group are provided additional protections against credential theft and tactics such as Kerberos abuse. |
| **Read-only Domain Controllers** | Contains all Read-only domain controllers in the domain. |
| **Remote Desktop Users** | This group is used to grant users and groups permission to connect to a host via Remote Desktop (RDP). This group cannot be renamed, deleted, or moved. |
| **Remote Management Users** | This group can be used to grant users remote access to computers via Windows Remote Management (WinRM). |
| **Schema Admins** | Members can modify the Active Directory schema, which is the way all objects with AD are defined. This group only exists in the root domain of an AD forest. The Administrator account for the forest root domain is the only member of this group by default. |
| **Server Operators** | This group only exists on domain controllers. Members can modify services, access SMB shares, and backup files on domain controllers. By default, this group has no members. |

---

## User Rights Assignment

Depending on their current group membership, and other factors such as privileges that administrators can assign via Group Policy (GPO), users can have various rights assigned to their account. This Microsoft article on User Rights Assignment provides a detailed explanation of each of the user rights that can be set in Windows. Not every right listed here is important to us from a security standpoint as penetration testers or defenders, but some rights granted to an account can lead to unintended consequences such as privilege escalation or access to sensitive files. 

For example, let's say we can gain write access over a Group Policy Object (GPO) applied to an OU containing one or more users that we control. In this example, we could potentially leverage a tool such as SharpGPOAbuse to assign targeted rights to a user. We may perform many actions in the domain to further our access with these new rights. A few examples include:

| Privilege | Description |
|-----------|-------------|
| **SeRemoteInteractiveLogonRight** | This privilege could give our target user the right to log onto a host via Remote Desktop (RDP), which could potentially be used to obtain sensitive data or escalate privileges. |
| **SeBackupPrivilege** | This grants a user the ability to create system backups and could be used to obtain copies of sensitive system files that can be used to retrieve passwords such as the SAM and SYSTEM Registry hives and the NTDS.dit Active Directory database file. |
| **SeDebugPrivilege** | This allows a user to debug and adjust the memory of a process. With this privilege, attackers could utilize a tool such as Mimikatz to read the memory space of the Local System Authority (LSASS) process and obtain any credentials stored in memory. |
| **SeImpersonatePrivilege** | This privilege allows us to impersonate a token of a privileged account such as NT AUTHORITY\SYSTEM. This could be leveraged with a tool such as JuicyPotato, RogueWinRM, PrintSpoofer, etc., to escalate privileges on a target system. |
| **SeLoadDriverPrivilege** | A user with this privilege can load and unload device drivers that could potentially be used to escalate privileges or compromise a system. |
| **SeTakeOwnershipPrivilege** | This allows a process to take ownership of an object. At its most basic level, we could use this privilege to gain access to a file share or a file on a share that was otherwise not accessible to us. |

There are many techniques available to abuse user rights detailed here and here. Though outside the scope of this module, it is essential to understand the impact that assigning the wrong privilege to an account can have within Active Directory. A small admin mistake can lead to a complete system or enterprise compromise.

---

## Viewing a User's Privileges

After logging into a host, typing the command `whoami /priv` will give us a listing of all user rights assigned to the current user. Some rights are only available to administrative users and can only be listed/leveraged when running an elevated CMD or PowerShell session. These concepts of elevated rights and User Account Control (UAC) are security features introduced with Windows Vista that default to restricting applications from running with full permissions unless absolutely necessary. If we compare and contrast the rights available to us as an admin in a non-elevated console vs. an elevated console, we will see that they differ drastically. First, let's look at the rights available to a standard Active Directory user.

### Domain Admin Rights Non-Elevated

We can see the following in a non-elevated console which does not appear to be anything more than available to the standard domain user. This is because, by default, Windows systems do not enable all rights to us unless we run the CMD or PowerShell console in an elevated context. This is to prevent every application from running with the highest possible privileges. This is controlled by something called User Account Control (UAC) which is covered in-depth in the Windows Privilege Escalation module.
