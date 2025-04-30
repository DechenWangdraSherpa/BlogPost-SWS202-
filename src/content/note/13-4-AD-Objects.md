---
title: 13-4-AD Objects
seriesId: 13-Active-Directory
publishDate: "2025-04-29T14:16:00Z"
---

# Active Directory (AD) Objects
##  What Is an Object in AD?

- Definition: Any resource in an AD environment.
- Examples: Users, Groups, Computers, OUs, Printers, Domain Controllers.
- Object Types:

    - Leaf Objects: Cannot contain other objects (e.g., users, computers).
    - Container Objects: Can contain other objects (e.g., groups, OUs).

## User Objects

- Type: Leaf Object & Security Principal
- Has: SID + GUID
- Common Attributes:
   - Display name, email, last login, password last set, manager,
   - address
- Security Note:
   - Valuable to attackers (even low-privileged users)
   - Over 800 possible attributes in large environments

## Contact Objects

- Type: Leaf Object
- NOT a Security Principal
- Has: GUID only (no SID)
- Used For: Representing external users (e.g., vendors)
- Attributes: Name, email, phone, company

## Printer Objects

- Type: Leaf Object
- NOT a Security Principal
- Has: GUID only
- Attributes: Name, driver, port, location

## Computer Objects

- Type: Leaf Object & Security Principal
- Has: SID + GUID
- Used For: Workstations or servers joined to the domain
- Security Note:
    - Valuable to attackers (can be used to escalate privileges using NT AUTHORITY\SYSTEM)

## Shared Folder Objects

- Type: Leaf Object
- NOT a Security Principal
- Has: GUID only
- Attributes:
    - Folder name, path, access control list (ACL)

- Security Tip:

   - Access control ranges from public to strictly restricted

## Group Objects

- Type: Container Object & Security Principal
- Has: SID + GUID
- Purpose: Simplify permission management
- Features:
    - Can contain users, computers, even other groups (nested groups)
    - Used to manage access (e.g., Remote Management group)
- Tool for Audit: BloodHound (visualizes group relationships and nested memberships)
- Common Attributes: Name, description, members, parent groups

## Organizational Units (OUs)

- Type: Container Object
- NOT a Security Principal
- Used For: Structuring and delegating AD administration
- Features:
   - Can contain users, groups, computers
   - Often mirror company departments (e.g., HR, IT)
- Benefits:
   - Delegate tasks (e.g., reset passwords for specific users)
   - Apply specific Group Policies at the OU level
- Attributes: Name, members, linked GPOs, permissions

## Domain

- Definition: The structural boundary in AD.
- Contains: Users, computers, groups, OUs
- Each Domain Has:
   - Its own database
   - Its own default and custom policies (e.g., password policy)

## Domain Controllers (DCs)

- Role: Central servers that:
   - Handle authentication and authorization
   - Enforce security policies
   - Store information about all AD objects

## Sites

- Definition: Logical groupings of computers across subnets.
- Used For:
   - Optimizing AD replication
   - Managing large networks with multiple physical locations

## Built-in Container

- Definition: Stores default AD groups created automatically.
- Examples: Administrators, Users, Backup Operators

## Foreign Security Principals (FSPs)

- Definition: Placeholder objects for accounts from trusted external forests.
- Has: SID (from foreign forest) + GUID
- Created When:
   - An external user/group/computer is added to a local AD group
- Location:
   - Stored in the ForeignSecurityPrincipals container
   - Example DN: CN=ForeignSecurityPrincipals,DC=example,DC=com