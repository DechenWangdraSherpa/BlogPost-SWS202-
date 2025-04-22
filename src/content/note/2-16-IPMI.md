---
title: 2-16-IPMI
seriesId: 2-Footprinting
publishDate: "2025-04-22T07:30:00Z"
---

# IPMI (Intelligent Platform Management Interface)

## Overview:
**IPMI** is a standardized specification used for hardware-based host management and monitoring. It operates independently of the host's BIOS, CPU, firmware, and operating system, allowing **system administrators (sysadmins)** to manage and monitor systems even if the host is powered off or unresponsive.

### Key Features:
- **Remote Management**: Allows remote management of systems without requiring physical access to the target host.
- **Hardware Monitoring**: Can monitor system temperature, voltage, fan status, power supplies, and more.
- **Post-Failure Access**: Provides access to the system even after a failure, such as a crash or power off.
- **Pre-OS Configuration**: Enables modification of BIOS settings before the OS has booted.
- **Network Access**: Operates over a direct network connection to the system's hardware.

IPMI provides a way to perform tasks such as powering off or upgrading systems remotely, and viewing hardware logs. It is used extensively in enterprise environments for its robustness.

## Components Required for IPMI:
1. **Baseboard Management Controller (BMC)**: The central micro-controller responsible for implementing IPMI.
2. **Intelligent Chassis Management Bus (ICMB)**: An interface that facilitates communication across chassis.
3. **Intelligent Platform Management Bus (IPMB)**: Extends the BMC for further communication.
4. **IPMI Memory**: Stores system event logs and repository data.
5. **Communication Interfaces**: These include serial and LAN interfaces, ICMB, and PCI Management Bus for communication between components.

## Footprinting the Service:
- **Port 623 UDP**: IPMI communicates over this port.
- **BMC (Baseboard Management Controller)**: BMCs are typically embedded ARM systems running Linux, and they are connected to the host's motherboard.
- Most servers have built-in BMCs, with common brands like **HP iLO**, **Dell DRAC**, and **Supermicro IPMI**.
  
### Scanning BMCs:
- If a BMC is accessible, it gives nearly the same level of access as physical access to the system, allowing sysadmins to monitor, reboot, power off, or reinstall the OS.
- Many BMCs expose web-based management consoles or allow access through protocols such as Telnet or SSH.

Example Nmap scan for IPMI service footprinting:
```bash
nmap --script ipmi-version <target-ip>
