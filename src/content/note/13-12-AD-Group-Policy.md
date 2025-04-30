---
title: 13-12-AD Group Policy
seriesId: 13-Active-Directory
publishDate: "2025-04-30T16:12:00Z"
---

# Examining Group Policy

Group Policy is a Windows feature that provides administrators with a wide array of advanced settings that can apply to both user and computer accounts in a Windows environment. Every Windows host has a Local Group Policy editor to manage local settings. For our purposes, we will focus on Group Policy in a domain context for managing users and computers in Active Directory. Group Policy is a powerful tool for managing and configuring user settings, operating systems, and applications. Group Policy is also a potent tool for managing security in a domain environment.

From a security context, leveraging Group Policy is one of the best ways to widely affect your enterprise's security posture. Active Directory is by no means secure "out of the box," and Group Policy, when used properly, is a crucial part of a defense-in-depth strategy. 

While Group Policy is an excellent tool for managing the security of a domain, it can also be abused by attackers. Gaining rights over a Group Policy Object could lead to lateral movement, privilege escalation, and even full domain compromise if the attacker can leverage them in a way to take over a high-value user or computer. They can also be used as a way for an attacker to maintain persistence within a network. Understanding how Group Policy works will give us a leg up against attackers and can help us greatly on penetration tests, sometimes finding nuanced misconfigurations that other penetration testers may miss.

## Group Policy Objects (GPOs)

A Group Policy Object (GPO) is a virtual collection of policy settings that can be applied to user(s) or computer(s). GPOs include policies such as screen lock timeout, disabling USB ports, enforcing a custom domain password policy, installing software, managing applications, customizing remote access settings, and much more. Every GPO has a unique name and is assigned a unique identifier (a GUID). They can be linked to a specific OU, domain, or site. A single GPO can be linked to multiple containers, and any container can have multiple GPOs applied to it. They can be applied to individual users, hosts, or groups by being applied directly to an OU. Every GPO contains one or more Group Policy settings that may apply at the local machine level or within the Active Directory context.

### Example GPOs

Some examples of things we can do with GPOs may include:
- Establishing different password policies for service accounts, admin accounts, and standard user accounts using separate GPOs.
- Preventing the use of removable media devices (such as USB devices).
- Enforcing a screensaver with a password.
- Restricting access to applications that a standard user may not need, such as cmd.exe and PowerShell.
- Enforcing audit and logging policies.
- Blocking users from running certain types of programs and scripts.
- Deploying software across a domain.
- Blocking users from installing unapproved software.
- Displaying a logon banner whenever a user logs into a system.
- Disallowing LM hash usage in the domain.
- Running scripts when computers start/shutdown or when a user logs in/out of their machine.

Let's use as an example a default Windows Server 2008 Active Directory implementation, where password complexity is enforced by default. The password complexity requirements are as follows:
- Passwords must be at least 7 characters long.
- Passwords must contain characters from at least three of the following four categories:
  - Uppercase characters (A-Z)
  - Lowercase characters (a-z)
  - Numbers (0-9)
  - Special characters (e.g. !@#$%^&*()_+|~-=`{}[]:";'<>?,./)

These are just a few examples of what can be done with Group Policy. There are hundreds of settings that can be applied within a GPO, which can get extremely granular. For example, below are some options that we can set for Remote Desktop sessions.

## RDP GPO Settings

GPO settings are processed using the hierarchical structure of AD and are applied using the **Order of Precedence** rule as seen in the table below:

### Order of Precedence

| Level                                  | Description                                                                 |
|----------------------------------------|-----------------------------------------------------------------------------|
| **Local Group Policy**                 | The policies are defined directly to the host locally outside the domain. Any setting here will be overwritten if a similar setting is defined at a higher level. |
| **Site Policy**                        | Any policies specific to the Enterprise Site that the host resides in. Example: Access Control policies for a specific research site. |
| **Domain-wide Policy**                 | Settings applied across the domain as a whole. Example: setting the password policy complexity level. |
| **Organizational Unit (OU)**          | Settings applied to users and computers in specific OUs. Example: role-specific settings like mapping shared drives for HR or IT admins. |
| **Any OU Policies nested within other OU's** | Settings for objects within nested OUs. Example: providing Security Analysts a specific set of Applocker policy settings. |

We can manage Group Policy from the **Group Policy Management Console** (found under Administrative Tools in the Start Menu on a domain controller), custom applications, or using the PowerShell GroupPolicy module via the command line. 

The **Default Domain Policy** is the default GPO that is automatically created and linked to the domain. It has the highest precedence of all GPOs and is applied by default to all users and computers. Generally, it is best practice to use this default GPO to manage default settings that will apply domain-wide. The **Default Domain Controllers policy** is also created automatically with a domain and sets baseline security and auditing settings for all domain controllers in a given domain. It can be customized as needed, like any GPO.

### GPO Order of Precedence

GPOs are processed from the top down when viewing them from a domain organizational standpoint. A GPO linked to an OU at the highest level in an Active Directory network (at the domain level, for example) would be processed first, followed by those linked to a child OU, etc. This means that a GPO linked directly to an OU containing user or computer objects is processed last. In other words, a GPO attached to a specific OU would have precedence over a GPO attached at the domain level because it will be processed last and could run the risk of overriding settings in a GPO higher up in the domain hierarchy. 

One more thing to keep track of with precedence is that a setting configured in **Computer policy** will always have a higher priority of the same setting applied to a user.

### GPO Precedence Order

Let’s look at another example using the Group Policy Management Console on a Domain Controller. In this image, we see several GPOs. The **Disabled Forced Restarts GPO** will have precedence over the **Logon Banner GPO** since it would be processed last. Any settings configured in the Disabled Forced Restarts GPO could potentially override settings in any GPOs higher up in the hierarchy (including those linked to the Corp OU).

#### GPMC Hive Example

This image also shows an example of several GPOs being linked to the **Corp OU**. When more than one GPO is linked to an OU, they are processed based on the **Link Order**. The GPO with the lowest Link Order is processed last, or the GPO with link order 1 has the highest precedence, then 2, and 3, and so on. 

If the **Enforced** option is set, policy settings in GPOs linked to lower OUs **CANNOT** override the settings. If a GPO is set at the domain level with the **Enforced** option selected, the settings contained in that GPO will be applied to all OUs in the domain and cannot be overridden by lower-level OU policies.

### Enforced GPO Policy Precedence

Regardless of which GPO is set to enforced, if the **Default Domain Policy GPO** is enforced, it will take precedence over all GPOs at all levels.

#### Default Domain Policy Override

It is also possible to set the **Block inheritance** option on an OU. If this is specified for a particular OU, then policies higher up (such as at the domain level) will NOT be applied to this OU.

### Block Inheritance

Group Policy Refresh Frequency:
- By default, Windows performs periodic Group Policy updates every 90 minutes with a randomized offset of +/- 30 minutes for users and computers. The period is only 5 minutes for domain controllers.
- The **gpupdate /force** command can be issued to force an immediate update of Group Policy.

## Security Considerations of GPOs

GPOs can be used to carry out attacks. These attacks may include adding additional rights to a user account, adding a local administrator to a host, creating a scheduled task to run a malicious command, or even installing targeted malware throughout a domain. These attacks typically happen when a user has the rights required to modify a GPO that applies to an OU that contains either a user account that they control or a computer.

Below is an example of a GPO attack path identified using the **BloodHound** tool. This example shows that the **Domain Users** group can modify the **Disconnect Idle RDP GPO** due to nested group membership.

---

