# Enterprise Security Operations Center (SOC) & Threat Simulation Homelab

## Project Overview
This project involved architecting and deploying a distributed, multi-node virtualized Security Information and Event Management (SIEM) environment using **Wazuh (XDR/SIEM)**. The primary objective was to establish deep endpoint visibility on a modern corporate workstation, engineer defensive detection controls, and validate those controls by simulating real-world adversary behavior. 

By modeling both offensive actions (Red Team) and defensive telemetry engineering (Blue Team), this lab demonstrates a full-lifecycle approach to modern detection engineering, incident analysis, and system hardening.

---

## Network Architecture & Topology

The lab is built upon an isolated virtual network environment using Oracle VirtualBox. It utilizes a three-pillar architecture to isolate production telemetry and simulate an enterprise attack surface.

| Machine | Operating System | Role | IP Address (Bridged) | Telemetry / Tools Installed |
| :--- | :--- | :--- | :--- | :--- |
| **Wazuh Manager** | Ubuntu / Linux | Distributed SIEM Brain | `192.168.200.32` | Wazuh Indexer, Dashboard, Server |
| **Windows Target** | Windows 11 Enterprise | Evaluation Workstation | Dynamic (Bridged) | Wazuh Agent, Microsoft Sysmon |
| **Kali Linux** | Kali Linux | Attack Simulator | Dynamic (Bridged) | Nmap, Custom Command Utilities |

### Environmental Data Flow Diagram
```text
[ Kali Linux (Attacker) ] --(Simulated Brute Force)--> [ Windows 11 Workstation (Target) ]
                                                                      │
                                                   (Sysmon & Wazuh Agent Telemetry)
                                                                      ▼
[ Windows Host Web Browser ] <---(HTTPS:443)--- [ Distributed Wazuh SIEM Manager (Brain) ]
