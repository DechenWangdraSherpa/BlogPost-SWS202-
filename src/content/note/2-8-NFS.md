---
title: 2-8-NFS
seriesId: 2-Footprinting
publishDate: "2025-04-22T01:05:00Z"
---

# NFS (Network File System)

## Overview
NFS is a network file system developed by Sun Microsystems, designed for sharing file systems over a network as if they were local. Unlike SMB, which is typically used between Windows systems, NFS is primarily used between Linux and Unix systems. The main goal of NFS is to allow file access and sharing across different machines in a network, but it uses a different protocol.

### Key Features:
- **Cross-System File Sharing**: NFS is used for file sharing between Linux/Unix systems, but it cannot directly communicate with SMB servers.
- **Distributed File System**: NFS enables distributed file systems where files can be accessed and managed across multiple systems, providing a uniform view of the files.
- **Authentication**: While NFSv3 provides client authentication, NFSv4 introduces user authentication, similar to SMB in Windows environments.

## NFS Versions

| Version   | Features |
|-----------|----------|
| **NFSv2** | Older version, supports many systems but was initially designed to operate entirely over UDP. |
| **NFSv3** | Introduced more features like variable file sizes and better error reporting. However, it is not fully compatible with NFSv2 clients. |
| **NFSv4** | Includes Kerberos authentication, works through firewalls, supports ACLs, and improves performance. It also introduced stateful operations and simplified usage by eliminating the need for portmappers. |
| **NFSv4.1** | Extends NFSv4 with features for clustered server deployments and parallel file access across multiple servers (pNFS). Also includes session trunking (NFS multipathing). |

## Key Features of NFSv4
- **Kerberos Authentication**: NFSv4 includes Kerberos for user authentication.
- **Firewall Compatibility**: Unlike previous versions, NFSv4 works seamlessly through firewalls and on the Internet.
- **ACL Support**: NFSv4 supports Access Control Lists (ACLs) for finer-grained permission control.
- **Stateful Protocol**: NFSv4 is the first version to have a stateful protocol, which improves performance and reliability.
- **Single Port for Communication**: NFSv4 uses only **TCP/UDP port 2049**, simplifying the protocol's use across firewalls.

## Authentication and Authorization
- NFS uses the **Open Network Computing Remote Procedure Call (ONC-RPC)** protocol, which operates over **TCP/UDP port 111**.
- Authentication and authorization in NFS are handled by the RPC protocol, not by NFS itself.
- The server translates the client's user information into the file system's format using **UID/GID** and group memberships.
- One potential issue is that the client and server may not have the same **UID/GID** mappings, which could lead to authorization problems. Thus, NFS should only be used in trusted networks where UID/GID mappings are consistent.

## Configuration
- NFS is relatively simple to configure compared to protocols like FTP and SMB.
- The **/etc/exports** file on the NFS server lists the file systems that are shared and the clients that can access them.
- The **NFS Exports Table** defines the accessible file systems and the specific options for access control.

## Key Takeaways:
- **Cross-System Communication**: NFS is primarily for Linux and Unix systems, enabling file sharing and access in distributed environments.
- **Version Improvements**: Each version of NFS has introduced new features like better authentication, support for firewalls, and performance improvements.
- **Security Considerations**: Authentication is handled through RPC, with UID/GID mappings being crucial for proper access control.
- **Ease of Configuration**: NFS has a simpler configuration process compared to other file-sharing protocols, relying on the **/etc/exports** file to manage shared resources.
