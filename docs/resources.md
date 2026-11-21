# Lab Resource Overview

## 1. Host budget

| Resource | Total | Notes |
|---|---|---|
| RAM | 12 GB | Windows 11 host baseline is approximately 3 to 4 GB |
| Free disk | approximately 70 GB | Dynamic VM disks grow on use, up to declared maximum |

## 2. Per-VM allocation (observed in VirtualBox)

| Hostname | vCPU | RAM | Disk (declared) | Typical actual usage |
|---|---|---|---|---|
| SIEM-01 | 2 | 3.5 GB | 30 GB dynamic | 15 to 20 GB with Wazuh and indexer |
| LNX-ENDPOINT-01 | 1 | 2 GB | 20 GB dynamic | 5 to 7 GB |
| WIN-ENDPOINT-01 | 2 | 3.5 GB | 25 GB dynamic | 12 to 15 GB |
| ATTACK-01 | 1 | 2 GB | 20 GB dynamic | 5 to 10 GB depending on tool install |
| Total declared | 6 | 11 GB | 95 GB dynamic | approximately 37 to 52 GB actual |

The "typical actual usage" column is an estimate, not a measurement. It will be
replaced with real values as the lab progresses.

## 3. Simultaneous operation analysis

Running all four simultaneously:

- RAM: 11 GB of VM RAM plus 3 to 4 GB for the Windows 11 host is 14 to 15 GB,
  which exceeds the 12 GB available.
- vCPU: 6 virtual CPUs against a typical host with 4 to 8 logical cores.
  Contention is likely but not fatal.
- Disk: 37 to 52 GB actual usage against 70 GB free. Tight but feasible.

Conclusion: all four cannot run simultaneously on this host.

## 4. Recommended operating strategy

| Combination | VMs running | Total VM RAM | Feasible |
|---|---|---|---|
| A | SIEM-01, LNX-ENDPOINT-01 | 5.5 GB | Yes |
| B | SIEM-01, WIN-ENDPOINT-01 | 7 GB | Yes |
| C | SIEM-01, ATTACK-01, LNX-ENDPOINT-01 | 7.5 GB | Yes, with the host otherwise idle |
| D | SIEM-01, ATTACK-01, WIN-ENDPOINT-01 | 9 GB | At the limit; only if the host is otherwise idle |
| E | All four | 11 GB | No |

Recommended for normal work: A, B or C. Combination D is usable for a Windows
simulation when no other heavy work is running on the host. Combination E is
not supported by this host.

## 5. SIEM-01 evaluation

SIEM-01 runs at 2 vCPU and 3.5 GB. This is below the Wazuh recommended baseline,
which assumes a dedicated node. It is the configuration that fits this host.
Do not reduce it further. If indexing slows during a simulation, reduce the
number of simultaneous endpoints rather than the SIEM RAM.

## 6. Disk caution

70 GB free is workable for the current declared disks if actual usage stays
near the estimates in Section 2. It is not workable if SIEM-01's Wazuh index
grows without retention limits. Two mitigations are in scope:

- Set a Wazuh index retention or rotation policy on SIEM-01.
- Remove old VirtualBox snapshots when they are no longer needed.

Any disk-exhaustion incident is recorded in `docs/troubleshooting/`.

## 7. Trade-offs and alternatives

If the host is later expanded:

- Additional RAM would allow combinations D and E comfortably.
- A second physical disk would remove the disk ceiling.
- A dedicated SIEM host would allow SIEM-01 to meet Wazuh's recommended sizing.

None of these are in scope for the current phase. The lab continues within the
sequential operating model in Section 4.
