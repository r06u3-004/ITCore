# ITCore

### IT Infrastructure Operations & Diagnostics Platform

ITCore is a local platform designed for **enterprise IT infrastructure operations, diagnostics, monitoring, incident management, alerting, and reporting**.

It provides infrastructure engineers, system administrators, network engineers, and IT support teams with a centralized operational interface for investigating and managing infrastructure events.

The operational workflow is:

> **Observe → Correlate → Diagnose → Report → Escalate**

---

## Overview

ITCore is designed to operate across enterprise infrastructure environments containing:

* Windows servers
* Linux servers
* Workstations
* Active Directory
* DNS
* DHCP
* File services
* Application services
* Database services
* Network infrastructure
* Users and sessions
* Enterprise services
* Infrastructure dependencies

The initial implementation is built around a single Python script:

```text
ITCore.py
```

The script provides the main operational interface and contains the infrastructure discovery, diagnostic, monitoring, incident, alerting, and reporting logic.

---

# Infrastructure Operations

ITCore provides a centralized operational view of the infrastructure.

The platform is designed to answer operational questions such as:

* Which systems are currently available?
* Which systems are unreachable?
* Which services are running?
* Which services have failed?
* Which users are connected?
* Which privileged accounts are active?
* Is the problem related to the network?
* Is the server reachable?
* Is the application service available?
* Which users are affected?
* Which incidents are currently active?
* Who needs to be notified?

---

# Systems

ITCore provides system-level diagnostics and operational information.

Capabilities include:

* Systems overview
* Systems inventory
* System status
* System information
* CPU utilization
* Memory utilization
* Storage
* Filesystems
* Running processes
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

The objective is to provide infrastructure engineers with a consolidated view of system state instead of requiring individual tools for every diagnostic step.

---

# Users

ITCore provides operational visibility into users and sessions.

Capabilities include:

* Users overview
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

User states are represented explicitly:

```text
ACTIVE
IDLE
CONNECTED
DISCONNECTED
LOGGED OFF
UNKNOWN
```

An unreachable system is not automatically considered logged off.

Where the operating system exposes the required information, login and session timestamps can be recorded with second-level precision.

---

# Network Operations

ITCore provides network diagnostics for infrastructure operations and troubleshooting.

Capabilities include:

* Network overview
* Network discovery
* Network devices
* Network interfaces
* IP configuration
* Routing table
* ARP table
* DNS diagnostics
* DHCP diagnostics
* Gateway diagnostics
* Ping
* Traceroute
* TCP/UDP connectivity tests
* Ports and sockets
* Network connections
* VLAN information
* Network health
* Network diagnostics

The diagnostic workflow can correlate multiple network observations.

For example:

```text
Interface
    ↓
IP configuration
    ↓
Gateway
    ↓
DNS
    ↓
Remote connectivity
    ↓
Application connectivity
```

This allows ITCore to identify the infrastructure layer where a failure is occurring.

---

# Infrastructure

ITCore provides a global infrastructure view.

The infrastructure layer can aggregate information such as:

```text
Total Systems
Windows Servers
Linux Servers
Workstations
Network Infrastructure

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

ITCore distinguishes between:

```text
ONLINE
UNREACHABLE
OFFLINE
```

Network unreachability alone is not treated as definitive proof that a system is powered off.

Historical monitoring and `last seen` information can improve infrastructure-state determination.

---

# Active Directory

ITCore provides operational visibility for Active Directory environments.

The platform is designed to monitor and diagnose areas such as:

* Domain controllers
* Domain availability
* Domain users
* Privileged accounts
* User sessions
* Authentication events
* Failed logins
* Directory-related services
* Infrastructure health

Active Directory events can also participate in the incident and alerting workflow.

---

# Diagnostic Engine

ITCore uses deterministic diagnostics to correlate infrastructure observations.

The objective is not simply to report that a command failed, but to determine the relevant infrastructure layer.

Example:

```text
Interface DOWN
      ↓
Interface problem
```

```text
Interface UP
      ↓
No IP address
      ↓
IP / DHCP problem
```

```text
IP available
      ↓
Gateway unreachable
      ↓
Network / gateway problem
```

```text
Gateway reachable
      ↓
DNS resolution fails
      ↓
DNS problem
```

```text
Network OK
      ↓
Server reachable
      ↓
Application service DOWN
      ↓
Service / application incident
```

This correlation provides the infrastructure engineer with operational context for troubleshooting.

---

# Incident Management

ITCore provides an incident-management layer for infrastructure events.

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

An incident can therefore combine:

```text
Infrastructure
      +
System
      +
Network
      +
Service
      +
Users
      ↓
Incident
```

---

# Alerts & Escalation

ITCore provides an alerting and escalation layer for infrastructure events.

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

Recovery events can generate a corresponding notification:

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

# Monitoring

ITCore can operate continuously to detect infrastructure state changes.

Start monitoring with:

```bash
python3 ITCore.py --monitor
```

On Linux:

```bash
sudo python3 ITCore.py --monitor
```

Monitoring can detect events such as:

* Systems becoming unavailable
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

Continuous monitoring also enables historical state tracking.

---

# Reports

ITCore provides operational reporting capabilities.

Reports can cover:

* Infrastructure
* Systems
* Users
* Network
* Incidents
* Security / administrators
* Infrastructure health
* Exportable operational information

Reports provide a consolidated view of the environment for troubleshooting, operational follow-up, and documentation.

---

# Security Model

ITCore is designed to operate with administrative privileges where required by the operating system.

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

The initial operational model prioritizes **read-only diagnostics and observation**.

Administrative actions are treated separately and should require explicit confirmation.

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

Potential administrative actions include:

* Restarting services
* Stopping processes
* Disabling accounts
* Modifying network configuration
* Modifying firewall configuration
* Changing system configuration

These operations should never be executed silently.

---

# Usage

The main application is:

```text
ITCore.py
```

Run the platform with:

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

The monitoring process observes infrastructure state and records relevant state transitions.

---

# Screenshots

The following screenshots illustrate the main operational interfaces of ITCore.

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

The initial repository is intentionally simple:

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

The initial application is entirely contained in:

```text
ITCore.py
```

The script is internally organized into functional components while remaining deployable as a single file.

---

# Development Approach

ITCore is developed around a real-world enterprise infrastructure model.

Development and validation are performed in a controlled environment before deployment against production infrastructure.

The development process follows three main stages.

### Enterprise Infrastructure Design

Define the infrastructure architecture, systems, users, services, network topology, dependencies, and operational scenarios.

### ITCore.py Development

Implement the operational capabilities required to observe, diagnose, monitor, report, and manage infrastructure events.

### ITCore.py Improvement

Continuously improve the platform based on infrastructure scenarios, diagnostic requirements, monitoring results, and operational use cases.

---

# Operational Workflow

ITCore follows a centralized infrastructure-operations workflow:

```text
                    INFRASTRUCTURE
                          │
          ┌───────────────┼───────────────┐
          │               │               │
       SYSTEMS          USERS           NETWORK
          │               │               │
          └───────────────┼───────────────┘
                          │
                     OBSERVATION
                          │
                      CORRELATION
                          │
                       DIAGNOSIS
                          │
                       INCIDENT
                          │
                ┌─────────┴─────────┐
                │                   │
              REPORT              ALERT
                                    │
                               ESCALATION
                                    │
                                TELEGRAM
```

The objective is to give infrastructure teams the operational context required to understand:

* What is happening?
* Where is the problem?
* Which systems are affected?
* Which users are affected?
* Which infrastructure layer is failing?
* How severe is the event?
* What evidence supports the diagnosis?
* Who should be notified?

---

# Project Vision

ITCore aims to provide a practical operational platform for:

* Helpdesk engineers
* System administrators
* Network engineers
* Infrastructure engineers
* IT operations teams
* Incident responders

The platform brings together systems, users, networks, services, incidents, monitoring, alerts, and reporting into a single operational workflow.

The long-term objective is to provide an infrastructure operations layer capable of **observing the environment, correlating events, identifying failures, documenting incidents, and escalating critical events** while keeping administrative actions controlled and auditable.

---

# Author

**r06u3**


---

## License

This project is licensed under the terms defined in the repository's `LICENSE` file.
