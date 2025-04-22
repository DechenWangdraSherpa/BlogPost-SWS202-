---
title: 2-10-SMTP
seriesId: 2-Footprinting
publishDate: "2025-04-22T01:55:50Z"
---

# SMTP (Simple Mail Transfer Protocol)

## Overview
SMTP is the protocol used for sending emails in an IP network. It facilitates communication between an email client and an outgoing mail server, or between two SMTP servers. While SMTP handles sending emails, it is often combined with IMAP or POP3 for receiving and managing emails. SMTP operates as a client-server protocol but can also involve one server acting as a client to another server.

## Ports Used
- **Port 25**: Default port for SMTP communication.
- **Port 587**: Used for authenticated connections with STARTTLS encryption, securing the email transmission.
- **Port 465**: Occasionally used for encrypted connections with SSL/TLS (less common).

## Unencrypted SMTP
SMTP sends emails in plaintext by default, including commands and authentication information, which can be intercepted. To secure the connection, **SSL/TLS encryption** is applied, either using **STARTTLS** or by connecting through port 465.

## Components of SMTP
- **Mail User Agent (MUA)**: The client that sends the email, also known as the email client.
- **Mail Submission Agent (MSA)**: Relays the email from the MUA to the SMTP server and verifies the origin of the email.
- **Mail Transfer Agent (MTA)**: Sends and forwards the email from one server to another. It may be susceptible to attacks like Open Relay if misconfigured.
- **Mail Delivery Agent (MDA)**: Delivers the email to the recipient's mailbox.
- **Mailbox**: Managed by protocols like **POP3** or **IMAP**, which allow users to retrieve and manage their emails.

## SMTP Flow:

Client (MUA) ➞ Submission Agent (MSA) ➞ Open Relay (MTA) ➞ Mail Delivery Agent (MDA) ➞ Mailbox (POP3/IMAP)


## Common SMTP Commands

| Command       | Description |
|---------------|-------------|
| **AUTH PLAIN** | Used for authenticating the client with a user name and password. |
| **HELO**       | The client logs in with its computer name and starts the session. |
| **MAIL FROM**  | The client specifies the email sender. |
| **RCPT TO**    | The client specifies the email recipient. |
| **DATA**       | The client initiates the transmission of the email. |
| **RSET**       | The client aborts the current email transmission but keeps the connection open. |
| **VRFY**       | The client verifies if a mailbox is available for message transfer. |
| **EXPN**       | The client checks if a mailbox is available for messaging. |
| **NOOP**       | The client requests a response from the server to prevent disconnection due to timeout. |
| **QUIT**       | The client terminates the session. |

## Security Measures
- **ESMTP**: Extended SMTP includes **STARTTLS**, which upgrades a plain connection to an encrypted one.
- **SMTP-Auth**: Authentication mechanism used to prevent unauthorized email sending.
- **Spam Prevention**: Measures like **SPF** (Sender Policy Framework) and **DKIM** (DomainKeys Identified Mail) help to secure email transmission and prevent spoofing.
- **Open Relay Attack**: Misconfigured SMTP servers can be exploited as open relays for sending spam. Proper configuration is essential to prevent this.

## Disadvantages of SMTP
1. **No Delivery Confirmation**: SMTP does not provide a usable delivery confirmation by default. Although the protocol allows for this, its format is not standardized, typically returning only an error message in English.
2. **Lack of Authentication**: SMTP does not authenticate the sender, which allows for mail spoofing and the misuse of open SMTP relays for sending spam. This can be mitigated with proper configuration and security measures (e.g., ESMTP, authentication, and anti-spam protocols).

## Default SMTP Configuration
SMTP servers can be configured with various settings to control how emails are sent and processed. Some key commands include:
- **HELO**: Client login command.
- **MAIL FROM**: Specifies the sender.
- **RCPT TO**: Specifies the recipient.
- **DATA**: Starts the email transmission.
- **QUIT**: Ends the session.

### SMTP and Telnet
To interact with an SMTP server, a tool like **Telnet** can be used to initialize a TCP connection. Commands like **HELO** or **EHLO** are used to start the SMTP session.
