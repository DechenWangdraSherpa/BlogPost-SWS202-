---
title: 13-3-AD Terminology
seriesId: 13-Active-Directory
publishDate: "2025-04-29T13:50:00Z"
---

# Active Directory (AD) Terminology
## Key Concepts
### Authentication

- Purpose: Verifying a user’s identity (e.g., using a username and password).

- Analogy: Like showing your ID at a secure building entrance.

### Authorization

- Purpose: Granting access to resources based on permissions.

- Analogy: Like being allowed into specific rooms of a building after your ID is verified.

## Core Components of Active Directory
### Domain

- Definition: A logical grouping of network objects (users, computers, printers) sharing a central directory database.
- Example: yourcompany.com
- Key Role: Primary administrative boundary in AD.

### Domain Controller (DC)

- Definition: A server that stores and manages the AD database (Active Directory Domain Services).
- Functions:
    - Authenticates users.
    - Enforces security policies.
    - Replicates AD data to other DCs.

### Forest

- Definition: The top-level container that holds one or more AD domains.
- Purpose: Represents the entire AD infrastructure.
- Notes:
  - Domains in a forest share a schema and global catalog.
  - First domain in a forest is called the forest root domain.

### Tree

- Definition: A collection of one or more domains in a contiguous namespace.
- Example:

    - Parent: company.com
    - Child: sales.company.com

## Objects in Active Directory
### Object

- Definition: Any entity stored in AD (e.g., users, computers, groups).

### Organizational Unit (OU)

- Definition: A container for organizing AD objects within a domain.
- Benefits:
    - Easier delegation of administrative tasks.
    - Simplifies Group Policy management.

### User Account

- Definition: An object representing a person or service that can authenticate and access domain resources.

### Computer Account

- Definition: Represents a computer in the domain.

### Group

- Definition: A collection of users/computers for simplified permission management.

##  Infrastructure and Services
### Group Policy

- Definition: A feature for centrally managing and configuring OS, application, and user settings in AD.
- Example: Automatically locking a computer after 10 minutes of inactivity.

### Trust

- Definition: A relationship that allows users in one domain to access resources in another.
- Types:
   - One-way or Two-way
   - Transitive or Non-transitive

##  Directory and Replication
### Schema

- Definition: Defines the structure of AD — object classes and their attributes.
- Note: Shared across the forest and rarely changed.

### Global Catalog

- Definition: A distributed data repository with a searchable subset of all objects in the forest.
- Used For: Locating objects quickly, especially in multi-domain forests.

### Replication

- Definition: The process of synchronizing AD data between domain controllers.
- Goal: Ensure all DCs have consistent and up-to-date data.