---
title: 2-6-FTP
seriesId: 2-Footprinting
publishDate: "2025-04-21T23:05:00Z"
---

# FTP and TFTP

## FTP (File Transfer Protocol)

FTP is one of the oldest and most widely used protocols on the Internet. It operates at the **application layer** of the TCP/IP protocol stack, the same layer as protocols like HTTP and POP. FTP enables the transfer of files between clients and servers, and while modern browsers and email clients support it, there are also specialized FTP programs for more advanced operations.

### How FTP Works

When an FTP connection is established, two communication channels are opened:

1. **Control Channel (TCP Port 21)**: This is used for sending commands from the client to the server and receiving responses from the server, including status codes indicating whether commands were successful.
2. **Data Channel (TCP Port 20)**: This is used exclusively for data transfer between the client and server. The protocol monitors for errors during the transfer process and can resume the transfer if the connection is interrupted.

### Active vs Passive FTP

There are two modes of FTP operation:

- **Active FTP**: In active mode, the client initiates the connection via TCP port 21 and informs the server of which client-side port it will use for the data channel. However, if a firewall is present on the client side, it may block the server’s attempt to respond.
  
- **Passive FTP**: In passive mode, the server announces a port through which the client can initiate the data channel. Since the client makes the connection, this avoids the problem caused by firewalls blocking the server’s attempts to connect.

### FTP Commands and Status Codes

FTP supports various commands and status codes to manage file transfers and directory structures. Common commands include uploading and downloading files, organizing directories, and deleting files. The server responds to each command with a status code, indicating whether the action was successful.

### FTP Security Considerations

- **Clear-text Protocol**: FTP sends data, including login credentials, in clear text, making it susceptible to **sniffing** if the network conditions allow.
- **Anonymous FTP**: Some FTP servers allow anonymous FTP access, where no login credentials are required. However, this introduces security risks, and typically, only limited actions (like downloading public files) are allowed on such servers.

## TFTP (Trivial File Transfer Protocol)

TFTP is a simplified version of FTP, designed for file transfers between client and server processes. It lacks many of the features found in FTP, including user authentication.

### Key Differences from FTP

- **No Authentication**: TFTP does not require user authentication, making it less secure than FTP. It operates based on the read and write permissions of files in the operating system, without protected login mechanisms like passwords.
  
- **Uses UDP**: Unlike FTP, which uses TCP, TFTP uses **UDP**, a connectionless and unreliable protocol. This means that TFTP lacks the reliability mechanisms of FTP, relying on **UDP-assisted application layer recovery** to handle errors.

- **Limited Use**: Due to the lack of security, TFTP is generally used only in local, protected networks where the risks of exposure are minimized.

### Use Cases

TFTP is typically used in environments where simple file transfers are needed, such as in **local networks** or situations where **authentication and security** are not a concern. Its use is often limited to transferring files that are openly shared and accessible by all users in the network.
