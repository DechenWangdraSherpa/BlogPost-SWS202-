---
title: 13-11-Security in Active Directory
seriesId: 13-Active-Directory
publishDate: "2025-04-30T15:50:00Z"
---

# Security in Active Directory

Active Directory (AD) is inherently designed for central management and quick data sharing across a broad user base, making it prone to vulnerabilities by default. Ensuring proper security for AD requires balancing the **CIA Triad** (Confidentiality, Integrity, and Availability), with a tendency toward **Availability** and **Confidentiality**. To strengthen AD, Microsoft provides built-in features and practices to mitigate common attack vectors.

Here are the core **Active Directory Hardening Measures**:

---

## 1. Microsoft Local Administrator Password Solution (LAPS)
- **Purpose**: Randomizes and rotates local administrator passwords to prevent lateral movement in a network.
- **Benefit**: Reduces the impact of a compromised host.
- **Frequency**: Password rotation intervals can be set (e.g., every 12 or 24 hours).
- **Note**: LAPS is useful but should be combined with other security measures for a robust defense.

---

## 2. Audit Policy Settings (Logging and Monitoring)
- **Purpose**: Essential for detecting suspicious or unauthorized activities.
- **Examples**:
  - Unauthorized user/computer addition
  - Password changes
  - Abnormal Kerberos activity
  - Password spraying or privilege escalation attempts
- **Action**: Set up logging and monitoring tools to identify unusual behaviors in AD.

---

## 3. Group Policy Security Settings
- **Purpose**: Use Group Policy Objects (GPOs) to enforce security policies across users, groups, and computers.
- **Key Settings**:
  - **Account Policies**: Password rules, account lockout policies, and Kerberos settings.
  - **Local Policies**: Security event audits, user rights assignments (permissions for hosts), and network access control.
  - **Software Restriction Policies**: Controls what software is allowed to run.
  - **Application Control Policies**: Restrict access to certain executables like PowerShell or CMD.
  - **Advanced Audit Policy Configuration**: Detailed audit settings for file access, logon/logoff events, privilege usage, etc.

---

## 4. Update Management (SCCM/WSUS)
- **Purpose**: Proper patch management to ensure critical security updates are applied across the network.
- **Tools**:
  - **WSUS**: Windows Server Update Services—automates patch management for Windows systems.
  - **SCCM**: System Center Configuration Manager—extends WSUS with additional features.

---

## 5. Group Managed Service Accounts (gMSA)
- **Purpose**: Automates password management for service accounts used in non-interactive services or tasks.
- **Benefit**: More secure than traditional service accounts, as passwords are automatically generated and updated.

---

## 6. Security Groups
- **Purpose**: Simplify access control by grouping users based on roles or responsibilities.
- **Examples**: Domain Admins, Account Operators, Backup Operators.
- **Note**: Security groups allow for easier permission management and less granular user access.

---

## 7. Account Separation
- **Purpose**: Administrators should use separate accounts for regular tasks and administrative duties.
- **Benefit**: Limits the attack surface by ensuring administrative credentials are not exposed in day-to-day activities.

---

## 8. Password Complexity Policies, Passphrases, and 2FA
- **Purpose**: Ensure strong passwords to prevent easy attacks like password spraying.
- **Best Practices**:
  - **Passphrases** or **random passwords**.
  - **Minimum length**: 12 characters or more.
  - Implement **Multi-Factor Authentication (MFA)**, particularly for remote access (e.g., RDP).
  
---

## 9. Limiting Domain Admin Account Usage
- **Purpose**: Restrict Domain Admin usage to only essential tasks on Domain Controllers.
- **Benefit**: Minimizes risk if an attacker compromises a non-privileged host.

---

## 10. Periodically Auditing and Removing Stale Users and Objects
- **Purpose**: Regularly review AD for outdated accounts or unused objects.
- **Action**: Disable or remove accounts that are no longer in use to reduce potential attack vectors.

---

## 11. Auditing Permissions and Access
- **Purpose**: Periodically review user access and permissions.
- **Key Areas to Audit**:
  - **Admin group memberships**.
  - **File shares** and **resource access**.
  - **Local admin rights** and **RDP permissions**.

---

## 12. Using Restricted Groups
- **Purpose**: Manage group membership centrally using Group Policy.
- **Benefit**: Ensures only authorized users are members of high-privilege groups (e.g., Domain Admins, Enterprise Admins).

---

## 13. Limiting Server Roles
- **Purpose**: Separate roles like IIS and web applications from critical servers (e.g., Domain Controllers).
- **Benefit**: Reduces the attack surface by not hosting unnecessary services on sensitive servers.

---

## 14. Limiting Local Admin and RDP Rights
- **Purpose**: Tighten control over who has local admin and RDP rights.
- **Best Practice**: Only grant local admin or RDP access to necessary users and minimize overly broad access (e.g., Domain Users group).

---

### Additional Security Measures:
- **Hardening Tools**: Tools like **Microsoft Security Baselines** can provide specific security templates to secure AD environments.
- **Defense-in-depth Strategy**: Ensure comprehensive coverage by implementing multiple layers of defense (e.g., endpoint protection, network segmentation, security training).

---