---
title: UnderPass (HACKTHEBOX)
description: "This is a writeup for the machine UnderPass from hackthebox, which is a Linux machine with difficulty easy." 
publishDate: "2025-04-23T7:10:10Z"
tags: ["HTB", "LinuxMachine", "easyMachine"]
---

# Enumeration
Nmap Scans

![alt text](HTBImage/UnderPass/nmapscan.png)

So, from the nmap scan for service and version scan, there are two ports open **22 SSH**, **80 HTTP**

Let's see what's there in the website. 

![alt text](HTBImage/UnderPass/website.png)

Seems, nothing interesting. 

Let's do a UDP scan in the target machine.

![alt text](HTBImage/UnderPass/udpscan.png)

We found that 161 SNMP port is open.

Let’s try to enumerate SNMP protocol using snmpwalk tool

![alt text](HTBImage/UnderPass/enumerateSNMP.png)

Found an email for the user steve ends with underpass.htb. We also notice that **daloradius** server is running which is simply an advanced RADIUS web management application that shares access to the backend database.

Try to get to the daloradius server page, but we got 403 Forbidden

![alt text](HTBImage/UnderPass/notfound.png)

From the daloradius docs on Github we found a login page on this path **daloradius/app/users/login.php**

![alt text](HTBImage/UnderPass/loginpagefound.png)

Found another login page under the path **/daloradius/app/operators/login.php**

![alt text](HTBImage/UnderPass/anotherloginpage.png)

Tried Default credentials, which is mostly, 

username: administrator
password: radius

![alt text](HTBImage/UnderPass/defaultlogin.png)

We got in.

![alt text](HTBImage/UnderPass/homepage.png)

Let's look around the page, and here we found this hashed password for the user **svcMosh**

![alt text](HTBImage/UnderPass/usersvcMosh.png)

Used **CrackStation** to crack the hashes. 

![alt text](HTBImage/UnderPass/crackstation.png)

**underwaterfriends** this is our password for the user **svcMosh**

Let's **ssh** to this user. 

![alt text](HTBImage/UnderPass/sshintoTheUser.png)

Let’s cat out the user flag

![alt text](HTBImage/UnderPass/userflag.png)

# Privilege Escalation

Do sudo -l to see if we can run any binary as root

We can run /usr/bin/mosh-server with sudo

![alt text](HTBImage/UnderPass/privilege.png)

The server is giving us two things **port 60001** and a key **i+r956uKBWw3I3fWC3zuAQ**
 
Found in the **/usr/bin** path another binary called mosh-client it seems that it’s used to connect to the server,
If we try to connect to the localhost on the port given it’ll tellus that

![alt text](HTBImage/UnderPass/client.png)

So, lets make an environment variable with the key using **export**

![alt text](HTBImage/UnderPass/export.png)

We got the root access.

![alt text](HTBImage/UnderPass/gotaccess.png)

Lets cat out the root flag.

![alt text](HTBImage/UnderPass/rootflag.png)


![alt text](HTBImage/UnderPass/pwned.png)

# Learnings

- SNMP Enumeration: Used snmpwalk to find users and services like DaloRADIUS.

- Web Recon: Discovered hidden login paths via GitHub docs.

- Default Credentials: Logged in using common default creds (administrator : radius).

- Hash Cracking: Cracked user password from a hash using CrackStation.

- Initial Access: SSH access using cracked credentials.

- Privilege Escalation: Escalated to root using sudo mosh-server and environment variables.

# Reference

CyGeek. (n.d.). UnderPass Walkthrough - HackTheBox. Medium. https://medium.com/@CyGeek/underpass-walkthrough-hackthebox-a7f038767a19

### Tools Used
- nmap 
- snmpwalk
- browser
- CrackStation
- ssh
- mosh-server/mosh-client