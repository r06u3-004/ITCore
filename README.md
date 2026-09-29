# ITCore

### IT Infrastructure Operations & Diagnostics Platform

ITCore is a local-first platform designed to centralize **IT support, systems administration, network operations, infrastructure diagnostics, incident management, monitoring, alerting and operational reporting** from a single interface.

The project is built around a simple operational workflow:

> **Observe → Correlate → Diagnose → Report → Escalate**

ITCore is designed to simulate and operate against a realistic enterprise infrastructure, providing a practical environment for developing and testing IT infrastructure operations capabilities.

---

## Overview

ITCore brings together multiple infrastructure operations domains:

* Systems
* Users
* Networks
* Infrastructure
* Active Directory
* Services
* Incidents
* Alerts
* Escalation
* Monitoring
* Reports

The initial implementation is intentionally built around a single Python script:

```text
ITCore.py
```

The script acts as the main operational interface and progressively gains capabilities as the simulated infrastructure becomes more complex.

---

# Enterprise Infrastructure Simulation

Before connecting ITCore to a real production environment, the project uses a **simulated enterprise infrastructure**.

The objective is to reproduce the types of systems, users, network segments, services and incidents that an infrastructure engineer would encounter in a professional environment.

Conceptually:

```text
                         ENTERPRISE
                        INFRASTRUCTURE
                              │
             ┌────────────────┼────────────────┐
             │                │                │
          SERVERS         NETWORK           USERS
             │                │                │
      ┌──────┼──────┐    ┌────┼────┐      ┌───┼───┐
      │      │      │    │    │    │      │   │   │
     AD     DNS    APP   SW   FW   RTR   HR IT FIN
      │             │
      │          DATABASE
      │
   FILE SERVER
```

The simulated environment can contain:

### Servers

* Domain Controller
* DNS Server
* DHCP Server
* File Server
* Database Server
* Application Server
* Web Server
* Monitoring Server
* Linux infrastructure servers
* Windows infrastructure servers

### Network

* Core router
* Layer 3 switches
* Access switches
* Firewalls
* VLANs
* Trunks
* Routing
* DHCP
* DNS
* NAT
* ACLs
* VPN
* Network segments

### Users

Users can be organized according to realistic enterprise departments:

```text
Management
Finance
Human Resources
IT
Sales
Operations
Support
Security
```

Each user can have attributes such as:

* Username
* Department
* Role
* System
* Session
* Login time
* Session state
* Privilege level

---

# ITCore Architecture

ITCore sits above the simulated infrastructure as the operational layer.

```text
                         ENTERPRISE INFRASTRUCTURE
                                  │
          ┌───────────────────────┼───────────────────────┐
          │                       │                       │
       SYSTEMS                  USERS                  NETWORK
          │                       │                       │
          └───────────────────────┼───────────────────────┘
                                  │
                             OBSERVATION
                                  │
                             CORRELATION
                                  │
                              DIAGNOSIS
                                  │
                              INCIDENT
                                  │
                     ┌────────────┴────────────┐
                     │                         │
                   REPORT                    ALERT
                                               │
                                          ESCALATION
                                               │
                                           TELEGRAM
```

ITCore does not simply execute isolated commands.

The objective is to correlate information from different infrastructure layers.

For example:

```text
User reports application unavailable
                │
                ▼
          Check network
                │
                ▼
          Network OK
                │
                ▼
        Check application server
                │
                ▼
        Server reachable
                │
                ▼
       Application service DOWN
                │
                ▼
          Create incident
                │
                ▼
          Send escalation
```

---

# Main Operational Domains

## 1. Systems

ITCore provides visibility into Windows and Linux systems.

Capabilities include:

* Systems overview
* Systems inventory
* System status
* System information
* CPU
* Memory
* Storage
* Filesystems
* Processes
* Services
* Listening ports
* Network connections
* Operating system information
* Software inventory
* Windows systems
* Linux systems
* Active Directory
* System health
* System logs
* Full system diagnostics

---

## 2. Users

The user management layer provides visibility into accounts and sessions.

Capabilities include:

* All users
* Connected users
* Logged-off users
* Active sessions
* Disconnected sessions
* Login/logout history
* User activity
* Administrators
* Local administrators
* Domain administrators
* Privileged sessions
* Failed logins
* User diagnostics

ITCore distinguishes between:

```text
ACTIVE
IDLE
CONNECTED
DISCONNECTED
LOGGED OFF
UNKNOWN
```

An unreachable system is not automatically considered logged off.

Historical session information can be collected through continuous monitoring and state tracking.

---

# 3. Network

The network domain provides tools for infrastructure and connectivity diagnostics.

Capabilities include:

* Network overview
* Network discovery
* Network devices
* Interfaces
* IP configuration
* Routing table
* ARP table
* DNS diagnostics
* DHCP diagnostics
* Gateway diagnostics
* Ping
* Traceroute
* TCP/UDP tests
* Ports and sockets
* Network connections
* VLANs
* Trunks
* STP
* LACP
* Firewall / ACL
* VPN / IPsec
* Network health
* Network diagnostics

The simulated infrastructure can reproduce common enterprise networking concepts:

```text
VLAN
TRUNK
STP
LACP
ARP
DHCP
DNS
NAT
ROUTING
OSPF
BGP
ACL
VPN / IPsec
FIREWALL
QoS
WIRELESS
802.1X
```

The architecture is designed to eventually accommodate environments using:

* Cisco
* FortiGate
* Huawei
* MikroTik
* Juniper
* Aruba
* Ubiquiti
* VyOS

---

# 4. Incidents

ITCore provides a complete operational incident layer.

Capabilities include:

* Incident overview
* Active incidents
* Critical incidents
* Open incidents
* Incident history
* Incident creation
* Incident diagnostics
* Troubleshooting
* Affected systems
* Affected users
* Incident timeline
* Incident resolution
* Incident closure

Example:

```text
INC-000142
Database Server Failure

Severity: CRITICAL
System: DB01
IP: 10.10.1.31
Status: OPEN
Detected: 12:43:17

Network       OK
Server        ONLINE
PostgreSQL    DOWN
Disk          82%
CPU           18%
RAM           61%

Affected Users: 23
Affected Apps:  4
```

---

# 5. Alerts & Escalation

ITCore can generate operational alerts from infrastructure events.

Capabilities include:

* Alerts overview
* Active alerts
* Alert history
* Telegram notifications
* Telegram configuration
* Notification testing
* Notification rules
* Escalation rules
* Critical alerts
* Recovery alerts
* User alerts
* System alerts
* Network alerts
* Active Directory alerts
* Incident escalation

Example:

```text
🚨 CRITICAL INCIDENT

INC-000142
Database Server Failure

SYSTEM: DB01
IP: 10.10.1.31

Server       🟢 ONLINE
Network      🟢 OK
PostgreSQL   🔴 DOWN
Disk         🟡 82%
CPU          🟢 18%
RAM          🟢 61%

Affected users: 23
Affected apps: 4

Detected: 12:43:17
Severity: CRITICAL
```

Recovery notifications can provide the final state:

```text
✅ INCIDENT RESOLVED

INC-000142
DB01

PostgreSQL service unavailable

Detected: 12:43:17
Resolved: 12:51:42
Duration: 00:08:25

PostgreSQL: RUNNING

Affected users: 23
Status: RESOLVED
```

---

# 6. Infrastructure

The infrastructure domain provides a global operational view.

Capabilities include:

* Infrastructure overview
* Infrastructure discovery
* All systems
* Windows infrastructure
* Linux infrastructure
* Network infrastructure
* Active Directory infrastructure
* Infrastructure health
* Infrastructure map
* Infrastructure statistics

The overview can aggregate:

```text
Total Systems
Windows Servers
Linux Servers
Network Devices
Workstations

ONLINE
UNREACHABLE
OFFLINE

HEALTHY
WARNING
CRITICAL

Active Sessions
Idle Sessions
Disconnected Sessions

Active Incidents
```

ITCore distinguishes between **unreachable** and **confirmed offline** states.

A failed network connection alone should not be interpreted as proof that a machine is powered off.

---

# 7. Reports

ITCore provides operational reporting capabilities.

Reports can cover:

* Infrastructure
* Systems
* Users
* Network
* Incidents
* Security / administrators
* Infrastructure health
* Exportable operational data

The objective is to provide a consolidated operational picture for troubleshooting and infrastructure follow-up.

---

# Diagnostic Engine

The diagnostic engine uses deterministic rules and infrastructure observations.

The objective is to identify the infrastructure layer associated with a failure.

Example:

```text
INTERFACE DOWN
      │
      ▼
INTERFACE PROBLEM
```

```text
INTERFACE UP
      │
      ▼
NO IP ADDRESS
      │
      ▼
IP / DHCP PROBLEM
```

```text
IP AVAILABLE
      │
      ▼
GATEWAY UNREACHABLE
      │
      ▼
LAN / GATEWAY PROBLEM
```

```text
GATEWAY REACHABLE
      │
      ▼
DNS FAILURE
      │
      ▼
DNS PROBLEM
```

```text
NETWORK OK
      │
      ▼
SERVER REACHABLE
      │
      ▼
APPLICATION SERVICE DOWN
      │
      ▼
APPLICATION / SERVICE INCIDENT
```

The goal is to provide evidence-based diagnostics rather than simply reporting that a command failed.

---

# Monitoring

ITCore can operate continuously and maintain infrastructure state over time.

Start monitoring with:

```bash
python3 ITCore.py --monitor
```

On Linux:

```bash
sudo python3 ITCore.py --monitor
```

Monitoring can detect:

* Systems appearing
* Systems becoming unreachable
* Systems recovering
* User logins
* User logouts
* Privileged account activity
* Services stopping
* Services recovering
* Network interfaces going down
* Network interfaces recovering
* Resource thresholds
* Active Directory events
* Incident recovery

Continuous monitoring also makes it possible to build historical state information.

---

# Security Model

ITCore is designed to operate with administrative privileges where required.

### Windows

Run PowerShell or Command Prompt as Administrator:

```powershell
python ITCore.py
```

### Linux

Run with sudo when required:

```bash
sudo python3 ITCore.py
```

The initial platform prioritizes **read-only diagnostics**.

Potential administrative actions are treated separately:

```text
ADMIN PRIVILEGES
       │
       ▼
READ / DIAGNOSTICS
       │
       ▼
SENSITIVE ACTION
       │
       ▼
EXPLICIT CONFIRMATION
       │
       ▼
AUDIT
```

Future actions could include:

* Restarting services
* Stopping processes
* Disabling accounts
* Modifying network configuration
* Modifying firewall rules
* Changing system configuration

These operations should require explicit confirmation.

---

# Usage

The main application is:

```text
ITCore.py
```

Run:

```bash
python3 ITCore.py
```

Linux with administrative privileges:

```bash
sudo python3 ITCore.py
```

Windows:

```powershell
python ITCore.py
```

The application starts from the main operational menu:

```text
╔════════════════════════════════════════════════════════════════════╗
║                           ITCore                                   ║
║                IT Infrastructure Operations                        ║
╠════════════════════════════════════════════════════════════════════╣
║                                                                    ║
║  1. SYSTEMS                                                        ║
║  2. USERS                                                          ║
║  3. NETWORK                                                        ║
║  4. INCIDENTS                                                      ║
║  5. ALERTS & ESCALATION                                            ║
║  6. INFRASTRUCTURE                                                 ║
║  7. REPORTS                                                        ║
║  0. EXIT                                                           ║
║                                                                    ║
╚════════════════════════════════════════════════════════════════════╝
```

Select a domain to access its operational functions.

---

# Monitoring Usage

Continuous monitoring:

```bash
python3 ITCore.py --monitor
```

Linux:

```bash
sudo python3 ITCore.py --monitor
```

The monitoring mode observes the configured infrastructure and records state changes.

---

# Screenshots

The following screenshots illustrate the main operational interfaces of the platform.

### Main Menu

<p align="center">
  <img src="docs/screenshots/main-menu.png" alt="ITCore main menu" width="900">
</p>

### Infrastructure Overview

<p align="center">
  <img src="docs/screenshots/infrastructure-overview.png" alt="ITCore infrastructure overview" width="900">
</p>

### Systems

<p align="center">
  <img src="docs/screenshots/systems.png" alt="ITCore systems interface" width="900">
</p>

### Users

<p align="center">
  <img src="docs/screenshots/users.png" alt="ITCore users interface" width="900">
</p>

### Network

<p align="center">
  <img src="docs/screenshots/network.png" alt="ITCore network interface" width="900">
</p>

### Incidents

<p align="center">
  <img src="docs/screenshots/incidents.png" alt="ITCore incident management" width="900">
</p>

### Alerts & Escalation

<p align="center">
  <img src="docs/screenshots/alerts-escalation.png" alt="ITCore alerts and escalation" width="900">
</p>

### Reports

<p align="center">
  <img src="docs/screenshots/reports.png" alt="ITCore reports" width="900">
</p>

---

# Project Structure

The initial repository intentionally remains simple:

```text
ITCore/
│
├── ITCore.py
├── README.md
├── LICENSE
│
└── docs/
    └── screenshots/
        ├── main-menu.png
        ├── infrastructure-overview.png
        ├── systems.png
        ├── users.png
        ├── network.png
        ├── incidents.png
        ├── alerts-escalation.png
        └── reports.png
```

The entire initial application is contained in:

```text
ITCore.py
```

The script remains internally organized into functional components so that it can later evolve into a larger architecture if required.

---

# Development Roadmap

## 1. Enterprise Infrastructure Design

Design and simulate a realistic enterprise infrastructure with:

* Windows and Linux servers
* Workstations
* Active Directory
* DNS / DHCP
* Network devices
* VLANs
* Routing
* Firewalls
* Users and departments
* Enterprise services
* Infrastructure dependencies
* Failure scenarios

## 2. ITCore.py Development

Develop the initial ITCore platform around the simulated infrastructure.

The script progressively implements:

* Systems
* Users
* Network
* Infrastructure
* Diagnostics
* Incidents
* Alerts & escalation
* Reports
* Monitoring

## 3. ITCore.py Improvement

Continuously improve the platform by testing it against increasingly realistic infrastructure scenarios.

Improvements will focus on:

* Diagnostic accuracy
* Infrastructure correlation
* Monitoring
* Incident detection
* Historical state tracking
* Network diagnostics
* Reporting
* Telegram escalation
* Additional infrastructure integrations

---

# Project Vision

ITCore aims to become a practical **IT Infrastructure Operations platform** capable of bringing together the daily activities of:

* Helpdesk engineers
* System administrators
* Network engineers
* Infrastructure engineers
* IT operations teams
* Incident responders

The project starts with a controlled enterprise simulation and progressively evolves toward a platform capable of interacting with real infrastructure.

The objective is not simply to execute administrative commands, but to build an operational layer capable of understanding the relationship between:

```text
Systems
   +
Users
   +
Network
   +
Services
   +
Infrastructure
   ↓
Operational Context
   ↓
Diagnosis
   ↓
Incident
   ↓
Alert / Escalation
```

---

# Author

*r06u3**

---

## License

This project is licensed under the terms defined in the repository's `LICENSE` file.
