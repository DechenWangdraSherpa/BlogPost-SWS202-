---
title: 13-9-AD Groups
seriesId: 13-Active-Directory
publishDate: "2025-04-29T15:36:00Z"
---

# Active Directory Groups

## Overview:
- Groups are used to simplify management of rights and access by grouping users, computers, and contacts.
- Groups can become targets for attackers if misconfigured, as they may grant unintended privileges.

## Difference Between Groups and OUs:
- **Groups**: Used to assign permissions to resources (e.g., file shares, printers).
- **OUs**: Used to group objects for management and apply Group Policy settings.

---

## Group Types
1. **Security Groups**:
   - Assign permissions to resources (e.g., printers, file shares).
   - All members inherit permissions assigned to the group.
   
2. **Distribution Groups**:
   - Used by email applications for distributing messages (e.g., mailing lists).
   - Cannot assign permissions to resources.

---

## Group Scopes
1. **Domain Local Group**:
   - Manages permissions within a single domain.
   - Can contain users from other domains.
   - Cannot be nested in global groups.
   
2. **Global Group**:
   - Used across domains but can only contain users from its domain.
   - Can be nested in domain local and universal groups.

3. **Universal Group**:
   - Used across multiple domains in a forest.
   - Can contain users from any domain but triggers forest-wide replication on changes.

---

## Built-in vs Custom Groups
- **Built-in Groups**: Predefined groups like "Domain Admins" with specific roles (cannot contain other groups).
- **Custom Groups**: Organizations create these for specific needs (e.g., department or app-specific groups).

---

## Nested Group Membership
- Groups can be nested, leading to inherited permissions from higher-level groups.
- **BloodHound** is a tool to analyze nested group memberships and identify excessive privileges.

---

## Important Group Attributes:
- **cn**: Common Name (group name).
- **member**: List of group members (users, other groups).
- **groupType**: Defines the group type and scope.
- **memberOf**: Groups containing this group (for nested memberships).
- **objectSid**: Unique security identifier for the group.

---

## Penetration Testing Relevance:
- Misconfigured group memberships can lead to privilege escalation.
- Groups and nested group memberships are key targets for testers to uncover potential attack vectors.