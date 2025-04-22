---
title: 2-15-Orachle_TNS
seriesId: 2-Footprinting
publishDate: "2025-04-22T07:00:00Z"
---


# Oracle TNS (Transparent Network Substrate)

## Overview:
The **Oracle Transparent Network Substrate (TNS)** is a communication protocol used to facilitate communication between Oracle databases and client applications over networks. TNS was introduced as part of the **Oracle Net Services** suite and supports various networking protocols, including **TCP/IP**, **IPX/SPX**, and **UDP**. It is widely used in industries such as **healthcare**, **finance**, and **retail** due to its ability to manage large, complex databases. 

### Key Features:
- **Name Resolution**: Resolves database service names to network addresses.
- **Connection Management**: Manages connections between client and database.
- **Load Balancing**: Distributes connections to optimize performance.
- **Security**: Supports **SSL/TLS encryption** to secure data communication, protecting against unauthorized access.
- **IPv6 Support**: Supports the newer IPv6 protocol for networking.

TNS also provides tools for **performance monitoring**, **error reporting**, **workload management**, and **fault tolerance**.

## Default Configuration:
### Listener:
- By default, the TNS listener listens for incoming connections on **TCP/1521** (this port can be modified during installation).
- The listener supports multiple network protocols, including **TCP/IP**, **UDP**, **IPX/SPX**, and **AppleTalk**.
- It can be configured to listen on specific IP addresses or all available interfaces.

### Security:
- **Basic Authentication**: Uses hostnames, IP addresses, usernames, and passwords for client-server authentication.
- **Encryption**: The default configuration supports encryption for communication between client and server through **Oracle Net Services**.

### Configuration Files:
- **tnsnames.ora**: A client-side configuration file that contains the necessary details to connect to Oracle services.
  - Includes service names, network locations, and database names.
  - Example entry:
    ```text
    ORCL =
      (DESCRIPTION =
        (ADDRESS_LIST =
          (ADDRESS = (PROTOCOL = TCP)(HOST = 10.129.11.102)(PORT = 1521))
        )
        (CONNECT_DATA =
          (SERVICE_NAME = orcl)
        )
      )
    ```
- **listener.ora**: A server-side configuration file that defines the properties of the listener process that receives and forwards client requests to the appropriate Oracle database instance.

## Common Security Risks and Configurations:
- **Default Passwords**: 
  - Oracle 9 has the default password `CHANGE_ON_INSTALL`.
  - Oracle 10 has no default password.
  - **Oracle DBSNMP** uses a default password `dbsnmp`.
- **Finger Service**: In some cases, organizations still use the **finger service**, which may expose sensitive information if not properly secured.
- **Default Listener Port**: The default listener port (1521) is commonly targeted during attacks. Organizations may overlook changing it from the default.

## Example of `tnsnames.ora` File:
The `tnsnames.ora` file defines service names and their corresponding network addresses. Here’s an example of how a service entry might look:
```text
ORCL =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = 10.129.11.102)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVICE_NAME = orcl)
    )
  )
