---
title: Active Directory Basics
seriesId: THM
publishDate: "2025-04-16T20:53:00Z"
---

# What is Active Directory?
Microsoft's Active Directory (AD) is the backbone of the corporate world, serving as a centralized management system for:

* Users

* Devices

* Permissions

* Security policies

It simplifies administration in large corporate environments by providing a centralized point of control.

---
# Objectives
In this session, we aim to understand the core concepts of Active Directory. By the end, you'll be familiar with:

* What Active Directory is
* What an Active Directory Domain is
* The components of an Active Directory Domain
* Concepts of Forests and Domain Trusts
* ...and much more!

---
# Windows Domain
In a small business network with just a handful of computers and employees, it’s manageable to configure each machine manually—setting up user accounts and handling support directly on-site. However, as the organization grows—imagine 157 computers and 320 users spread across four offices—this manual approach quickly becomes impractical. To address this complexity, organizations turn to **Windows Domains**, which group users and computers under centralized administration. The key to this setup is **Active Directory (AD)**, a centralized repository that simplifies the management of users, computers, and policies across the network. At the heart of this system is the **Domain Controller (DC)**, a server that hosts and manages Active Directory services, enabling streamlined control, configuration, and security enforcement across all connected systems.

![alt text](notes-images/bebe5dfec0208bf563d01fa2dd1fb7a7.png)

## Advantages of a Configured Windows Domain

- **Centralized Identity Management**  
  All users across the network can be configured and managed from **Active Directory** with minimal effort, reducing repetitive tasks and improving consistency.

- **Managing Security Policies**  
  Security policies can be configured directly within **Active Directory** and applied across users and computers in the network, ensuring uniform and efficient policy enforcement.

## A Real-World Example of Active Directory

If this sounds a bit confusing, chances are you’ve already interacted with a **Windows Domain** in environments like your **school**, **university**, or **workplace**.

In such networks, you're typically given a **username and password** that you can use to log in on **any computer** across the campus or office. This works because each computer **forwards your login credentials to Active Directory** for authentication. Your credentials don’t need to be stored on every machine — **Active Directory handles it centrally**.

Additionally, **Active Directory enforces policies** such as **restricting access to control panel settings** or **removing administrative privileges**. These restrictions are deployed network-wide to maintain security and uniform user permissions.

---
# Active Directory

##  Core of a Windows Domain: Active Directory Domain Services (AD DS)

At the heart of any Windows Domain lies the **Active Directory Domain Services (AD DS)**. It acts as a **catalogue** that stores information about all "objects" on the network. These objects include:

- Users  
- Groups  
- Machines  
- Printers  
- Network Shares  
- And many more...

Let’s take a closer look at some of these objects:

---

### Users

Users are one of the most common object types in AD. They are considered **security principals**, which means:
- They can be **authenticated** by the domain.
- They can be **assigned privileges** to access resources like files, folders, or printers.

Users can represent:

- **People**: Real individuals in the organization (e.g., employees).
- **Services**: System services like **IIS** or **MSSQL** also require user accounts, known as **service accounts**, which have only the minimal privileges required to run the service.

---

###  Machines

Each computer that joins the domain becomes an object in AD. Machines are also **security principals** and are assigned accounts just like users.

- **Machine accounts** have limited rights within the domain.
- On the local machine, the machine account typically has **local administrator privileges**.
- These accounts are **not usually accessed by humans**, but if someone has the password, they can log in with it.
- **Passwords** for machine accounts are:
  - Automatically rotated
  - Typically **120 random characters**

**Naming convention**:  
Machine account names follow the format:  
`<COMPUTER_NAME>$`  
Example: A machine named `DC01` would have an account named `DC01$`.

---

###  Security Groups

**Security groups** in AD allow for collective management of permissions. Instead of assigning rights to each user individually, you can:

- Add users to a group  
- Assign permissions to the group  
- Let the users **inherit those permissions automatically**

Key features:
- Groups can include **users**, **machines**, and even **other groups**
- Groups are also **security principals**, meaning they can hold permissions on network resources

---

###  Common Default Security Groups

Here’s a table of some important default security groups in a Windows Domain:

| **Security Group** 	| **Description**                                                             	|
|------------------------|---------------------------------------------------------------------------------|
| **Domain Admins**  	| Full administrative privileges over the entire domain, including all DCs.  	|
| **Server Operators**   | Can manage Domain Controllers, but cannot modify admin group memberships.  	|
| **Backup Operators**   | Can access any file regardless of its permissions; used for backup tasks.  	|
| **Account Operators**  | Can create and modify other accounts in the domain.                         	|
| **Domain Users**   	| Contains all user accounts in the domain.                                   	|
| **Domain Computers**   | Contains all computer (machine) accounts in the domain.                     	|
| **Domain Controllers** | Contains all Domain Controllers (DCs) in the domain.                        	|



