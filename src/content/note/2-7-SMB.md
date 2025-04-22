---
title: 2-7-SMB
seriesId: 2-Footprinting
publishDate: "2025-04-21T23:50:00Z"
---

# SMB (Server Message Block) Protocol

## Overview
SMB is a client-server protocol used to facilitate access to shared files, directories, and network resources such as printers and routers. It also allows for the exchange of information between different system processes. Originally developed as part of OS/2 and LAN Manager, SMB became widely associated with Microsoft’s Windows operating systems and is a key component of file sharing and network communication within Windows networks.

### Key Features:
- **File and Resource Sharing**: SMB enables client systems to communicate with servers for accessing shared resources like files and printers.
- **Cross-Platform Communication**: SMB supports communication between devices running different versions of Windows and Linux/Unix (via **Samba**).
- **Access Control**: It uses **Access Control Lists (ACLs)** to control access to shared resources with fine-grained permissions (e.g., read, write, execute).
- **Three-Way Handshake**: SMB relies on TCP for communication, using the standard three-way handshake to establish a reliable connection between client and server.

## Samba and CIFS

### Samba
- Samba is an open-source implementation of the SMB/CIFS protocol that enables Unix-based systems (e.g., Linux) to communicate with Windows-based systems.
- **CIFS** (Common Internet File System) is a dialect of SMB primarily associated with SMB version 1. 
- Samba allows Unix/Linux systems to serve resources (e.g., files, printers) to Windows systems, effectively enabling cross-platform sharing.

### CIFS vs SMB Versions:
- **CIFS (SMB 1.0)**: A specific implementation of SMB, originally designed for Windows NT 4.0. Typically operates over **TCP ports 137, 138, 139**.
- **SMB 2.x and SMB 3.x**: Introduced by Microsoft to enhance performance, improve security, and provide new features such as encryption, caching, and multichannel support.

### SMB Versions:
| Version   | Features | Supported Systems |
|-----------|----------|-------------------|
| **CIFS**  | Communication via NetBIOS interface | Windows NT 4.0 |
| **SMB 1.0** | Direct connection via TCP | Windows 2000 |
| **SMB 2.0** | Performance upgrades, improved message signing, caching | Windows Vista, Windows Server 2008 |
| **SMB 2.1** | Enhanced locking mechanisms | Windows 7, Windows Server 2008 R2 |
| **SMB 3.0** | Multichannel connections, end-to-end encryption, remote storage access | Windows 8, Windows Server 2012 |
| **SMB 3.0.2** | Stability improvements | Windows 8.1, Windows Server 2012 R2 |
| **SMB 3.1.1** | Integrity checking, AES-128 encryption | Windows 10, Windows Server 2016 |

### Samba Features:
- **Active Directory Integration**: Starting with version 3.0, Samba can be a full member of an Active Directory domain, enabling centralized authentication and resource management.
- **Domain Controller**: Version 4.0 introduced the ability for Samba to function as an Active Directory domain controller, supporting centralized user management and authentication.
- **Daemons**: Samba operates several background programs (daemons) that handle different tasks:
  - `smbd`: The SMB server daemon for handling file and print services.
  - `nmbd`: The NetBIOS Name Server daemon that supports NetBIOS over TCP/IP.

### NetBIOS and WINS:
- **NetBIOS**: A programming interface developed by IBM to allow computers to share data on a network. SMB originally relied on NetBIOS to manage network connections.
- **WINS (Windows Internet Name Service)**: An enhancement to NetBIOS that resolves names of computers in a Windows network to their IP addresses, allowing for easier communication between systems.

## Key Takeaways:
- **Cross-Platform**: Samba enables file sharing and resource access between Unix/Linux and Windows systems using the SMB/CIFS protocol.
- **Version Differences**: Newer versions of SMB (2.0 and 3.0) offer improvements in security, performance, and functionality compared to the older SMB 1.0 (CIFS).
- **Security and Access Control**: SMB uses ACLs for managing access to shared resources, and newer versions provide advanced encryption and other security features.
