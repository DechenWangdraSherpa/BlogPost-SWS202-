---
title: 2-14-MSSQL
seriesId: 2-Footprinting
publishDate: "2025-04-22T02:50:00Z"
---

# MSSQL (Microsoft SQL Server)

## Overview:
Microsoft SQL (MSSQL) is a relational database management system developed by Microsoft. Unlike MySQL, MSSQL is **closed-source** and was initially designed to run on **Windows operating systems**. It is widely used in environments that rely on **.NET framework** for application development. Although MSSQL has versions that can run on **Linux** and **macOS**, it is most commonly found on **Windows** systems.

## MSSQL Clients:
- **SQL Server Management Studio (SSMS)**: A tool that comes with MSSQL or can be installed separately. SSMS is used for managing and configuring MSSQL databases.
  - It can be installed on any system, not just the server hosting MSSQL, making it possible for admins or developers to connect to the database from remote machines.
  - **Security Risk**: If SSMS is installed on a vulnerable machine, it may contain saved credentials that can be exploited to gain access to the MSSQL server.

## Dangerous Settings:
As with any service, MSSQL can be misconfigured, leading to security vulnerabilities. Common dangerous settings include:
1. **No Encryption**: MSSQL clients not using encryption to connect to the server.
2. **Self-Signed Certificates**: Using self-signed certificates for encryption can be dangerous because they are susceptible to spoofing.
3. **Named Pipes**: Enabling named pipes, which can be used for local communication but can also present a security risk if improperly configured.
4. **Weak or Default sa Credentials**: The **sa** (system administrator) account may still have default or weak credentials, leaving the system vulnerable to brute-force attacks.

## Footprinting the MSSQL Service:
To gather useful information about MSSQL servers, a **Nmap** scan can be used. By targeting the default MSSQL TCP port (1433), you can gather information about:
- **Hostname**
- **Database Instance Name**
- **MSSQL Version**
- **Named Pipe Configuration**

### Example Nmap Scan:
An Nmap scan can help you identify critical details about MSSQL:
```bash
nmap -p 1433 --script ms-sql-info <target>
