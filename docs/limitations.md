# Lab Limitations

## Purpose and design goals

The goal of this SOC lab is to demonstrate detection, correlation,
investigation and response. The priority is to build an environment that
supports those goals using the resources available, rather than to replicate a
production-scale SOC. This is a resource-constrained lab with only the
components needed for the current and planned phases.

## Environment constraints

The lab runs on a Windows 11 host with 12 GB of RAM and approximately 70 GB of
free disk. Four VMs are configured.

The main constraint is not Wazuh alone. It is running the Wazuh stack plus
Ubuntu Server, Windows Server 2019 and an Ubuntu simulation source on the same
host, alongside Windows 11.

## Operating model constraint

The four VMs declare 11 GB of RAM in total, which exceeds the host's 12 GB
budget once Windows 11 is loaded. All four cannot run at the same time.

The lab therefore operates in combinations:

- SIEM-01 + one endpoint
- SIEM-01 + ATTACK-01 + one endpoint

Simulation activities are sequenced. Running multiple simulations in parallel
on this host is not supported.

## Disk constraint

The 70 GB figure is free space on the host, not total capacity. Virtual disk
files are dynamic and grow on use. Total declared capacity across the four VMs
is 95 GB, so full growth is not feasible.

Two mitigations apply:

- Wazuh index retention on SIEM-01 should be set to keep the index bounded.
- Old VirtualBox snapshots should be removed when no longer needed.

If either is neglected, disk exhaustion becomes likely before the lab reaches
the end of its planned phases.

## Single-host dependency

The entire lab runs on one physical machine. If the host fails or needs to be
reinstalled, the lab goes with it. Snapshot discipline and evidence retention
matter more here than in a distributed lab, not less.

## Resource allocation approach

Resource allocations are not based on official vendor minimums. They are
sized to guarantee a working environment for building an end-to-end detection
workflow within the available resources. SIEM-01 in particular runs below
Wazuh's recommended sizing. It is not reduced further. If indexing slows, the
recommended response is to reduce the number of simultaneous endpoints rather
than the SIEM RAM.

## Operational limits

Because of the constraints above, the lab is used for scoped activities only:

- No high-volume or sustained load testing.
- No parallel multi-endpoint simulation campaigns.
- No long-running capture sessions that exceed available disk.
- No malware analysis in the current phase. If introduced later, it requires a
  separate policy and a separate isolated environment.

## Progress and evidence

Progress, findings and evidence are recorded in this repository. The Phase 1
telemetry validation checklist, the Windows and Linux telemetry baselines, the
lab safety policy and the naming convention are the authoritative references.
