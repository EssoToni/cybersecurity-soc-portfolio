# SOC-001 : Repeated Authentication Failures Followed by a Successful Lab Login

## Metadata

| Field | Value |
|---|---|
| **Case ID** | SOC-001 |
| **Title** | Repeated authentication failures followed by successful lab login |
| **Date opened (UTC)** | 2026-10-31 |
| **Date closed (UTC)** | |
| **Analyst** | <your name> |
| **Phase** | Phase 1 — Foundation |
| **Status** | Planned |
| **Severity** | Low (lab simulation) |
| **Verdict** | (pending) |
| **Related cases** | — |

## 1. Alert / Trigger

- **Alert source:** Wazuh (rules for repeated authentication failures; exact
  rule IDs to be recorded at capture time)
- **Alert text / rule description:** (to be recorded)
- **First seen (UTC):** (to be recorded)
- **Detection rule or query used:** (to be recorded)
- **Raw alert artifact:** EV-01 (planned)

## 2. Hypothesis

- **Hypothesis:** Repeated failed authentications from a single lab source
  followed by a successful authentication for the same account will produce a
  detectable Wazuh alert and a reconstructable timeline across endpoint and
  SIEM telemetry.
- **What would confirm it:** ≥ N failed auth events from ATTACK-01, a subsequent
  successful auth for the same account, both visible in endpoint logs and in
  Wazuh Discover, within the same UTC window.
- **What would refute it:** Failures not visible in Wazuh, successful login not
  linked to the same source, or no alert produced.

## 3. Scope and safety

- **Authorization:** [lab-safety.md](../../../docs/policies/lab-safety.md)
- **Target(s):** WIN-ENDPOINT-01, LNX-ENDPOINT-01
- **Source host:** ATTACK-01 (or SIEM-01 if ATTACK-01 not yet provisioned)
- **Lab segment:** host-only / internal
- **Pre-flight checklist completed:** pending
- **Snapshot name:** pending
- **Account used:** `labvictim` (to be created on both endpoints)

## 4. Environment

| Host | Role | OS | Agent status |
|---|---|---|---|
| SIEM-01 | Wazuh manager | Ubuntu | Active |
| WIN-ENDPOINT-01 | Windows endpoint | Windows 10 | Active |
| LNX-ENDPOINT-01 | Linux endpoint | Ubuntu | Active |
| ATTACK-01 | Simulation source | (TBD) | N/A |

**Telemetry validation reference:** TV-02, TV-03, TV-04, TV-05 (all PASS from
Phase 1).

## 5. Evidence

### 5.1 Evidence summary (planned)

| Evidence ID | Type | Description | Path |
|---|---|---|---|
| EV-01 | screenshot | Wazuh Discover: 4625 events from source | `evidence/screenshots/` |
| EV-02 | screenshot | Event Viewer detail of one 4625 | `evidence/screenshots/` |
| EV-03 | screenshot | Wazuh Discover: 4624 after the failures | `evidence/screenshots/` |
| EV-04 | log | Linux auth.log SSH failure lines | `evidence/logs/` |
| EV-05 | json | Exported Wazuh alert payload | `evidence/exports/` |

### 5.2 Key evidence details

(To be written at capture time.)

### 5.3 Gaps

(To be recorded at capture time.)

## 6. Timeline (UTC)

| # | Time (UTC) | Event | Host | User | Source | Evidence |
|---|---|---|---|---|---|---|
| TL-01 | | First failed auth | | labvictim | | EV-XX |
| TL-02 | | Nth failed auth | | labvictim | | EV-XX |
| TL-03 | | Successful auth | | labvictim | | EV-XX |
| TL-04 | | Wazuh alert observed | SIEM-01 | N/A | Wazuh | EV-XX |

## 7. MITRE ATT&CK mapping

| Tactic | Technique ID | Technique name | How it appears in this case | Evidence |
|---|---|---|---|---|
| Credential Access | T1110 | Brute Force | Repeated failed auths from one source | EV-XX |
| Initial Access | T1078 | Valid Accounts | Successful auth after failures | EV-XX |

## 8. Verdict

- **Verdict:** pending
- **Reasoning:** pending
- **Confidence:** pending

## 9. Response

- **Immediate actions taken:** pending
- **Containment / remediation steps (lab):** pending
- **What would be different in production:** pending
- **Escalation path:** pending

## 10. Improvements

| Area | Finding | Proposed change |
|---|---|---|
| Detection | pending | |
| Telemetry | pending | |
| Process | pending | |
| Documentation | pending | |

## 11. References

- Lab safety: [lab-safety.md](../../../docs/policies/lab-safety.md)
- Naming convention: [evidence-naming-convention.md](../../../docs/references/evidence-naming-convention.md)
- Windows cheat sheet: [windows-event-cheat-sheet.md](../../../docs/references/windows-event-cheat-sheet.md)
- Linux baseline table: [linux-event-baseline-table.md](../../../docs/references/linux-event-baseline-table.md)
- Evidence register: [evidence-register.csv](evidence-register.csv)