# SOC Lab Architecture

## 1. Purpose and scope

The lab is a small, isolated SOC environment for hands-on detection,
investigation and incident response practice. It runs on a single
Windows 11 host under VirtualBox and uses a private Host-Only network for all
lab traffic. There is no external attack surface and no exposure to production
or personal networks.

## 2. Physical host

| Field | Value |
|---|---|
| Machine | Windows 11 workstation |
| Role | SOC Analyst workstation |
| VirtualBox Host-Only adapter | VirtualBox Host-Only Ethernet Adapter |
| Adapter IPv4 | 192.168.56.1 / 255.255.255.0 |
| Adapter DHCP | Enabled, not used by VMs (all VMs are static) |
| Host RAM | 12 GB |
| Host free disk | approximately 70 GB |

The Windows 11 host is used to access the Wazuh Dashboard, manage VMs in
VirtualBox, run Wireshark against the Host-Only segment, administer endpoints
over SSH and RDP, and maintain the GitHub repository. It is not a monitored
endpoint and hosts no Wazuh agent.

## 3. Virtual machines

| Hostname | OS | Role | IP | vCPU | RAM | Disk | Monitoring |
|---|---|---|---|---|---|---|---|
| SIEM-01 | Linux, Wazuh 4.14.9 | Wazuh manager, indexer, dashboard | 192.168.56.10 | 2 | 3.5 GB | 30 GB dynamic | N/A (server) |
| LNX-ENDPOINT-01 | Ubuntu Server 24.04 | Linux endpoint | 192.168.56.20 | 1 | 2 GB | 20 GB dynamic | Wazuh agent |
| WIN-ENDPOINT-01 | Windows Server 2019 | Windows endpoint | 192.168.56.30 | 2 | 3.5 GB | 25 GB dynamic | Wazuh agent and Sysmon |
| ATTACK-01 | Ubuntu Server 24.04 | Simulation source | 192.168.56.40 | 1 | 2 GB | 20 GB dynamic | Not monitored |

ATTACK-01 is not a Wazuh-monitored endpoint. It is a controlled source of
simulation activity. Any future decision to monitor it would be a separate
architectural change and would require an inventory and telemetry-validation
update.

## 4. Network

- Segment: VirtualBox Host-Only, 192.168.56.0/24, mask 255.255.255.0.
- All four VMs use static IPs. The Host-Only adapter's DHCP is enabled but not
  used by the VMs.
- No VM uses Bridged, NAT or Internal Network for lab traffic.
- During simulation windows, no VM has an external route. NAT is attached only
  for maintenance (package installation, updates) outside simulation windows
  and is detached before any simulation begins.
- The Host-Only adapter is the only interface that connects the VMs to the
  Windows 11 host. It does not connect to the internet.

## 5. Communication flows

- LNX-ENDPOINT-01 and WIN-ENDPOINT-01 send Wazuh agent traffic to SIEM-01 on
  1514/tcp.
- SIEM-01 exposes the Wazuh Dashboard on 443/tcp and the Wazuh API on
  55000/tcp to the Windows 11 host.
- ATTACK-01 sends simulation traffic only to the endpoints, never to SIEM-01
  or to the Windows 11 host.
- The Windows 11 host reads dashboard and API traffic from SIEM-01.

## 6. Isolation boundary

The VirtualBox Host-Only segment is the isolation boundary. Nothing inside the
segment can reach the internet, and nothing outside can reach the segment.
Activity beyond that boundary is outside the scope of this lab and outside the
rules of engagement in `docs/policies/lab-safety.md`.

## 7. Operating model

The host has 12 GB RAM and approximately 70 GB free disk. Running all four VMs
simultaneously is not possible: the four VMs declare 11 GB RAM in total, before
Windows 11 is loaded. Sequential operation is the intended model. See
`docs/resources.md` for the full analysis and the recommended combinations.

## 8. Diagram

The four-VM topology is maintained as Mermaid source in
`docs/diagrams/lab-topology.md`, which renders directly on GitHub.

## 9. What this document does not claim

- ATTACK-01 is installed and network-ready. It has not been used in a live
  case.
- Phase 1 telemetry validation was performed against the three original VMs.
  ATTACK-01 has not undergone telemetry validation and is not monitored.
- Nothing here claims production equivalence.

## 10. Related documents

- `docs/resources.md`
- `docs/asset-inventory.md`
- `docs/baseline-status.md`
- `docs/limitations.md`
- `docs/policies/lab-safety.md`
- `docs/diagrams/lab-topology.md`
