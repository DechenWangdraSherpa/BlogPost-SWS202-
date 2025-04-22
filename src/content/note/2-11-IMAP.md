---
title: 2-11-IMAP/POP3
seriesId: 2-Footprinting
publishDate: "2025-04-22T02:00:50Z"
---

# IMAP (Internet Message Access Protocol) / POP3 (Post Office Protocol)

## IMAP (Internet Message Access Protocol)
IMAP allows online management of emails on a remote server. It is client-server-based and supports synchronization across multiple clients, making it ideal for managing email folders directly on the server.

### Key Features of IMAP:
- **Folder Management**: Supports hierarchical mailboxes and folder structures.
- **Multiple Client Access**: Synchronizes across multiple clients, providing a uniform view of emails.
- **Offline Mode**: Some email clients offer offline access with local copies of emails.
- **Server-Side Storage**: Emails remain on the server until explicitly deleted, reducing local storage needs.
- **Port**: Typically uses port 143 for unencrypted connections or port 993 for SSL/TLS encrypted connections.
- **Text-Based**: Uses text-based commands in ASCII format to interact with the server.

### IMAP Commands:
| Command        | Description |
|----------------|-------------|
| **LOGIN**      | User login with username and password. |
| **LIST**       | Lists all directories available to the user. |
| **CREATE**     | Creates a new mailbox with the specified name. |
| **DELETE**     | Deletes a mailbox. |
| **RENAME**     | Renames a mailbox. |
| **LSUB**       | Lists subscribed mailboxes. |
| **SELECT**     | Selects a mailbox to access its messages. |
| **UNSELECT**   | Exits the selected mailbox. |
| **FETCH**      | Retrieves specific data from a message. |
| **CLOSE**      | Removes messages with the "Deleted" flag. |
| **LOGOUT**     | Closes the IMAP connection. |

### IMAP Security:
- **Encryption**: By default, IMAP works unencrypted, but SSL/TLS encryption is often required for secure communication, usually on port 993.
- **Offline Mode**: Some clients allow offline work with emails and synchronize changes once the connection is reestablished.

## POP3 (Post Office Protocol)
POP3 allows users to retrieve and delete emails from a server but lacks the advanced management features of IMAP. Emails are typically downloaded to the client and removed from the server.

### Key Features of POP3:
- **Simple Retrieval**: POP3 retrieves and deletes emails from the server.
- **No Folder Management**: Does not support hierarchical mailbox structures.
- **Offline Access**: Emails are downloaded and can be accessed offline.
- **Port**: Typically uses port 110 for unencrypted communication or port 995 for SSL/TLS encrypted communication.

### POP3 Commands:
| Command        | Description |
|----------------|-------------|
| **USER**       | Identifies the user to the server. |
| **PASS**       | Authenticates the user with a password. |
| **STAT**       | Requests the number of emails saved on the server. |
| **LIST**       | Requests information about the size and number of emails. |
| **RETR**       | Requests an email by its ID. |
| **DELE**       | Deletes an email by its ID. |
| **CAPA**       | Requests the server's capabilities. |
| **RSET**       | Resets the state of the session. |
| **QUIT**       | Closes the POP3 connection. |

### POP3 Security:
- **Encryption**: POP3 typically works unencrypted, but SSL/TLS encryption can be used on port 995.
- **Lack of Folder Support**: POP3 does not allow advanced management of emails on the server side, unlike IMAP.

## Dangerous Settings for Both Protocols:
Certain misconfigurations in IMAP and POP3 can lead to security vulnerabilities, such as leaking passwords or allowing anonymous login. Some dangerous settings include:

| Setting                     | Description |
|-----------------------------|-------------|
| **auth_debug**               | Logs all authentication attempts, potentially revealing sensitive information. |
| **auth_debug_passwords**     | Logs passwords, which may be insecure. |
| **auth_verbose**             | Logs unsuccessful login attempts and their reasons. |
| **auth_anonymous_username** | Allows anonymous login if configured, leading to potential unauthorized access. |

## Footprinting the Service:
You can use **Nmap** to scan for open ports related to IMAP and POP3 services:

- **IMAP**: Port 143 (unencrypted) or 993 (SSL/TLS).
- **POP3**: Port 110 (unencrypted) or 995 (SSL/TLS).

Scanning these ports with Nmap can provide details about the server's capabilities, including whether it uses SSL/TLS encryption.

## Default Configuration
Both IMAP and POP3 are highly configurable, but improper configurations can lead to vulnerabilities. Administrators should ensure proper security settings, especially with SSL/TLS encryption for both protocols.
