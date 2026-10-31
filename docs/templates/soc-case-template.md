# SOC-XXX : <Case Title>

> Template. To be copied in `investigations/SOC-XXX-<slug>/case.md` and filled
> in.

## Metadata

| Field | Value |
|---|---|
| **Case ID** | SOC-XXX |
| **Title** | |
| **Date opened (UTC)** | |
| **Date closed (UTC)** | |
| **Analyst** | |
| **Phase** | Phase 1 : Foundation |
| **Status** | Planned / In progress / Closed |
| **Severity** | Informational / Low / Medium / High / Critical |
| **Verdict** | (set in section 8) |
| **Related cases** | |

## 1. Alert / Trigger

What started this case?

- **Alert source:** (Wazuh rule ID, Event Viewer, manual observation)
- **Alert text / rule description:**
- **First seen (UTC):**
- **Detection rule or query used:**
- **Raw alert artifact:** (Evidence ID, e.g. `EV-01`)

## 2. Hypothesis

A single falsifiable statement. The investigation either supports or refutes it.

- **Hypothesis:**
- **What would confirm it:**
- **What would refute it:**

## 3. Scope and safety

- **Authorization:** [lab-safety.md](../../../docs/policies/lab-safety.md)
- **Target(s):**
- **Source host:**
- **Lab segment:** host-only / internal
- **Pre-flight checklist completed:** yes / no
- **Snapshot name:**
- **Account used:** (lab account, not a real one)

## 4. Environment

| Host | Role | OS | Agent status |
|---|---|---|---|
| SIEM-01 | Wazuh manager | | |
| WIN-ENDPOINT-01 | Windows endpoint | | |
| LNX-ENDPOINT-01 | Linux endpoint | | |
| ATTACK-01 | Simulation source | | |

**Telemetry validation reference:** Phase 1 checklist items applicable to this
case: `TV-XX`, `TV-YY`.

## 5. Evidence

All artifacts follow
[evidence-naming-convention.md](../../../docs/references/evidence-naming-convention.md).
The authoritative index is `evidence-register.csv` in this folder.

### 5.1 Evidence summary

| Evidence ID | Type | Description | Path |
|---|---|---|---|
| EV-01 | screenshot | | `evidence/screenshots/…` |
| EV-02 | log | | `evidence/logs/…` |
| EV-03 | json | | `evidence/exports/…` |

### 5.2 Key evidence details

For each significant artifact, one short paragraph: what it shows, why it
matters, and what it does **not** prove.

- **EV-01:**
- **EV-02:**

### 5.3 Gaps

- Evidence that could not be captured, and why.
- Evidence that was expected but did not appear (record as a telemetry gap, not
  a negative finding).

## 6. Timeline (UTC)

Every entry is one observable event with a source and evidence reference.

| # | Time (UTC) | Event | Host | User | Source | Evidence |
|---|---|---|---|---|---|---|
| TL-01 | | | | | | EV-XX |
| TL-02 | | | | | | EV-XX |
| TL-03 | | | | | | EV-XX |

**Timeline rules**

- UTC only.
- One row per event; not merge multiple events into a single row.
- Every row has an evidence reference or an explicit "no evidence" note.
- Source-side and SIEM-side events are listed separately so a discrepancy
  (event on endpoint, missing in SIEM) is visible.

## 7. MITRE ATT&CK mapping

| Tactic | Technique ID | Technique name | How it appears in this case | Evidence |
|---|---|---|---|---|
| Credential Access | T1110 | Brute Force | | EV-XX |
| Initial Access / Persistence | T1078 | Valid Accounts | | EV-XX |

Mapping rules:

- Map only what the evidence supports. Not map a technique "because it seems
  related".
- If a technique is suspected but unproven, say so explicitly in the row.

## 8. Verdict

- **Verdict:** True Positive / Benign True Positive / False Positive / Inconclusive
- **Reasoning:** (2-4 sentences tying the verdict to specific evidence)
- **Confidence:** High / Medium / Low

### Verdict definitions used here

| Verdict | Meaning |
|---|---|
| **True Positive** | The alert fired on activity that matches the intended detection and the activity occurred as described. |
| **Benign True Positive** | The detection fired correctly, but the underlying activity was authorized/expected (e.g. an approved test). |
| **False Positive** | The detection fired, but the underlying activity did not occur as the rule assumed. |
| **Inconclusive** | Evidence is insufficient to decide. Never upgrade this to a positive/negative verdict without new evidence. |

## 9. Response

What did (or would) an analyst do next?

- **Immediate actions taken:**
- **Containment / remediation steps (lab):**
- **What would be different in production:**
- **Escalation path:**

Keep lab actions and hypothetical production actions clearly separated : a
reviewer must be able to tell which is which.

## 10. Improvements

What changes because of this case?

| Area | Finding | Proposed change |
|---|---|---|
| Detection | | |
| Telemetry | | |
| Process | | |
| Documentation | | |

Each improvement should be a concrete, checkable change, not "be more
careful".

## 11. References

- Lab safety: [lab-safety.md](../../../docs/policies/lab-safety.md)
- Naming convention: [evidence-naming-convention.md](../../../docs/references/evidence-naming-convention.md)
- Windows cheat sheet: [windows-event-cheat-sheet.md](../../../docs/references/windows-event-cheat-sheet.md)
- Linux baseline table: [linux-event-baseline-table.md](../../../docs/references/linux-event-baseline-table.md)
- Evidence register: [evidence-register.csv](evidence-register.csv)