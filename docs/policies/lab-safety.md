# Lab Safety and Rules of Engagement

**Version:** 1.0  
**Effective:** 2026-10-31  
**Owner:** EssoToni  
**Scope:** All simulations, experiments and evidence capture performed in the
cybersecurity-soc-portfolio lab.

## 1. Authorization statement

All activity documented in this repository is performed **exclusively** against
systems that I own, control, and operate, inside an isolated lab network. No
simulation targets any system, account, network or data that I do not own or
have explicit written permission to test.

## 2. Non-negotiable rules

1. **Owned and controlled targets only.** Every target host is a VM I created
   or a device I own. No exceptions.
2. **Isolated lab network.** Simulations run on a host-only or internal virtual
   network. No simulation traffic leaves the lab segment or reaches the internet,
   a corporate network, or a shared/home production network.
3. **No real credentials.** Simulations use dedicated lab accounts created for
   the purpose. Real accounts, real passwords, API keys and tokens are never
   used as simulation inputs.
4. **No real data.** No personal, client, employer or third-party data is
   introduced into the lab. Sample files, synthetic logs and self-generated
   activity only.
5. **No malware.** This phase does not involve malware samples. Any future
   phase that touches malicious code requires a separate written policy and an
   isolated analysis environment.
6. **No external services as targets.** The lab does not probe public IPs,
   public domains, cloud tenants, or third-party SaaS.
7. **Snapshot before, rollback after.** Every endpoint has a clean snapshot
   taken before a simulation. After evidence capture, the endpoint can be rolled
   back to that snapshot if necessary.
8. **Stop condition.** If any simulation begins to affect a system outside the
   lab, we stop immediately, disconnect the VM from the network, and record the
   incident in the troubleshooting record.

## 3. Lab network definition

| Component | Role | Network |
|---|---|---|
| SIEM-01 | Wazuh manager / indexer / dashboard | lab segment |
| WIN-ENDPOINT-01 | Windows endpoint (agent) | lab segment |
| LNX-ENDPOINT-01 | Linux endpoint (agent) | lab segment |
| ATTACK-01 | Simulation source host | lab segment |

### Operational network

The lab uses a single VirtualBox Host-Only network:

- Subnet: 192.168.56.0/24
- Mask: 255.255.255.0
- Host adapter address: 192.168.56.1
- VM addresses: 192.168.56.10, .20, .30, .40

This is RFC 1918 private addressing. It is the operational network. It is not
substituted in documentation and it is not renamed.

No VM has an external route during simulations. Bridged, NAT and Internal
Network adapters are not used. NAT may be attached temporarily for package
installation outside simulation windows and is detached before any simulation
begins.

### Documentation addressing

RFC 5737 reserves three ranges for documentation and examples:

- 192.0.2.0/24 (TEST-NET-1)
- 198.51.100.0/24 (TEST-NET-2)
- 203.0.113.0/24 (TEST-NET-3)

These ranges are used only for illustrative and synthetic documentation. They
are never assigned to any VM or host interface in this lab.

Use is limited to:

- Hypothetical external hosts in diagrams.
- Sanitized replacements for actual public IPv4 addresses in published
  evidence, when the original public IP must be concealed.
- Synthetic indicators in detection-engineering exercises.

A TEST-NET address in published evidence is either a substitution or a
synthetic value. It is never represented as an observed public IP unless it
actually is one.

### Evidence publication

Original evidence (raw logs, screenshots, PCAPs, exported events) is kept local
and unmodified. Published derivatives are reviewed:

- Operational lab addresses in 192.168.56.0/24 may be published as-is.
- Public IPs that are sensitive may be replaced with TEST-NET addresses.
  Substitutions are consistent across related evidence.
- Redaction of any field that affects interpretation is noted on the published
  artifact.
- Original-to-replacement mappings for public IPs stay local and are never
  published as a table.

## 4. Pre-simulation checklist

Before any simulation, confirm all of the following:

- [ ] Target is a VM I own and control.
- [ ] VM is on the isolated lab network (verify adapter settings).
- [ ] Clean snapshot exists and is named.
- [ ] Wazuh agent on the target is Active.
- [ ] Telemetry validation (Phase 1) is PASS for the target's log sources.
- [ ] Simulation uses a dedicated lab account, not a real one.
- [ ] Evidence folder and case ID are prepared.
- [ ] UTC clock is synchronized on all hosts.

If any item is unchecked, the simulation does not start.

## 5. Post-simulation checklist

- [ ] Evidence captured and named per the naming convention.
- [ ] Case file updated with timeline and verdict.
- [ ] Endpoint rolled back to the clean snapshot if necessary.
- [ ] Lab account used for the simulation is removed or disabled if necessary.
- [ ] No simulation artifacts left in production-like state.

## 6. Data handling

- Evidence is stored in the case folder under `investigations/`.
- Raw, unsanitized captures and documantation are kept local only and never pushed.

## 7. Disclosure

This lab is a learning environment. Nothing in this repository should be read
as a claim of production experience. Findings are lab findings, scoped to the
lab environment described above.

## 8. Change history

| Version | Date | Change |
|---|---|---|
| 1.0 | 2026-10-31 | Initial rules of engagement |