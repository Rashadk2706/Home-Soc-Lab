# Home SOC Lab

A virtualized home SOC lab built on a Dell PowerEdge R620 using Proxmox VE, Wazuh SIEM, Active Directory, Sysmon, and Atomic Red Team.

The lab was designed to simulate a small enterprise environment where security events can be generated, collected, detected, investigated, and documented.

## Architecture

![SOC Lab Architecture](diagrams/soc-lab-network.png)

## Lab Environment

| System   | Role                      | IP Address  |
| -------- | ------------------------- | ----------- |
| pfSense  | Firewall / Router         | 10.10.10.1  |
| SIEM-01  | Wazuh SIEM                | 10.10.10.5  |
| DC-01    | Active Directory / DNS    | 10.10.10.10 |
| WIN-10   | Windows Endpoint / Sysmon | 10.10.10.20 |
| KALI-ATK | Attack Simulation         | 10.10.10.99 |

All systems operate within an isolated virtual network running on Proxmox VE.

## Objectives

* Build an isolated enterprise style security environment
* Deploy and configure Wazuh SIEM
* Configure Active Directory and DNS
* Deploy Sysmon for Windows endpoint telemetry
* Forward Windows security and Sysmon events to Wazuh
* Simulate adversary techniques using Atomic Red Team
* Detect and investigate security events
* Map activity to MITRE ATT&CK techniques
* Document findings through incident reports

## Detection Workflow

```text
Atomic Red Team
       ↓
Windows Endpoint
       ↓
     Sysmon
       ↓
  Wazuh Agent
       ↓
   Wazuh SIEM
       ↓
Detection / Alert
       ↓
Investigation
       ↓
Incident Report
```

## MITRE ATT&CK Techniques Tested

| Technique | Description                        | Status |
| --------- | ---------------------------------- | ------ |
| T1003.001 | LSASS Memory                       | Tested |
| T1059.001 | PowerShell                         | Tested |
| T1547.001 | Registry Run Keys / Startup Folder | Tested |

## Example Detection

Security activity is generated on the Windows endpoint using Atomic Red Team and monitored through Sysmon and Wazuh.

Investigations focus on:

* Process creation
* Command-line activity
* Parent-child process relationships
* Windows event logs
* Sysmon telemetry
* Wazuh alerts
* MITRE ATT&CK technique mapping

## Incident Reports

Detailed investigations and evidence are available in the `incident-reports/` directory.

* [T1003.001 - LSASS Memory](incident-reports/T1003.001-lsass.md)
* [T1059.001 - PowerShell](incident-reports/T1059.001-powershell.md)
* [T1547.001 - Registry Run Keys](incident-reports/T1547.001-registry-run-keys.md)

## Documentation

* [Architecture](docs/architecture.md)
* [Deployment Guide](docs/deployment-guide.md)
* [Incident Response](docs/incident-response.md)


## Environment

Built and tested in a controlled home lab environment running Proxmox VE.

This project is intended for educational and defensive security research. All security testing was performed within the isolated lab environment.
