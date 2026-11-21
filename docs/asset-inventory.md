# Asset Inventory

Last updated: 2026-11-21

This inventory supersedes the placeholder version dated 2026-10-13.

## Physical host

| Field | Value |
|---|---|
| Machine | Windows 11 workstation |
| Role | SOC Analyst workstation |
| Host-Only adapter | VirtualBox Host-Only Ethernet Adapter |
| Host-Only IPv4 | 192.168.56.1 / 24 |
| RAM | 12 GB |
| Free disk | approximately 70 GB |
| Purpose | VirtualBox management, Wireshark, SSH and RDP, GitHub, Wazuh dashboard |

## Virtual machines

| Hostname | OS | Role | IP | vCPU | RAM | Disk | Monitoring | Status |
|---|---|---|---|---|---|---|---|---|
| SIEM-01 | Wazuh 4.14.9 (Linux) | Wazuh manager, indexer, dashboard | 192.168.56.10 | 2 | 3.5 GB | 30 GB dynamic | server | Running, verified |
| LNX-ENDPOINT-01 | Ubuntu Server 24.04 | Linux endpoint | 192.168.56.20 | 1 | 2 GB | 20 GB dynamic | Wazuh agent | Running, agent Active |
| WIN-ENDPOINT-01 | Windows Server 2019 | Windows endpoint | 192.168.56.30 | 2 | 3.5 GB | 25 GB dynamic | Wazuh agent and Sysmon | Running, agent Active |
| ATTACK-01 | Ubuntu Server 24.04 | Simulation source | 192.168.56.40 | 1 | 2 GB | 20 GB dynamic | not monitored | Running, no agent |

See `docs/architecture.md` for network relationships and `docs/resources.md` for the resource strategy.

## Tools

| Tool | Category | Version | Status | Notes |
|---|---|---|---|---|
| Wazuh manager, indexer, dashboard | SIEM | 4.14.9 | Working | On SIEM-01 |
| Wazuh agent (Linux) | Endpoint agent | 4.14.9 | Working | On LNX-ENDPOINT-01 and ATTACK-01 is not monitored; agent is installed only on LNX |
| Wazuh agent (Windows) | Endpoint agent | 4.14.9 | Working | On WIN-ENDPOINT-01 |
| Sysmon | Endpoint telemetry | (record installed version) | Working | On WIN-ENDPOINT-01 |
| Wireshark | Network analysis | (record installed version) | Working | On Windows 11 host |
| OpenVAS | Vulnerability management | not installed | planned | To be installed in a later phase |
| Python | Automation | (record installed version) | Working | Host and Linux VMs |
| Bash | Automation | system default | Working | Linux VMs |
| PowerShell | Automation | (record installed version) | Working | Windows 11 host and WIN-ENDPOINT-01 |

The parenthesised version fields are for the operator to fill in after checking
the installed versions. They are intentionally not guessed here.

## Existing projects

External repositories are listed at github.com/EssoToni. They are not part of
this lab.

## Evidence

Evidence is organized under `evidence/` for lab baseline work and under
`investigations/SOC-NNN/evidence/` for case-specific work. See
`docs/references/evidence-naming-convention.md`.
