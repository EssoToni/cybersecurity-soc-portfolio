# Evidence Naming Convention

**Version:** 1.0  
**Effective:** 2026-10-31  
**Applies to:** All evidence captured in `investigations/`.

## 1. Why this exists

Evidence that cannot be found, identified or traced back to a case is not
evidence : it is a file. A consistent naming scheme makes every artifact:

- **Traceable** : the filename encodes the case and the evidence item.
- **Sortable** : timestamps sort chronologically.
- **Unique** : no two artifacts collide.
- **Self-describing** : the filename alone tells a reviewer what it is.

## 2. Identifier scheme

### Case ID

Format: `SOC-NNN` (three digits, zero-padded).

- `SOC-001`, `SOC-002`, … `SOC-999`.
- Assigned sequentially. Never reused. Never renumbered.
- A closed case keeps its number forever.

### Evidence ID

Format: `EV-NN` (two digits, zero-padded), scoped **per case**.

- Within `SOC-001`: `EV-01`, `EV-02`, … `EV-99`.
- The same `EV-01` may exist in `SOC-002` : the case ID disambiguates.
- Evidence IDs are recorded in the case's `evidence-register.csv` before the
  file is captured.

### Timestamp

Format: `YYYY-MM-DDTHHMMZ` : **UTC**, no separators inside the time.

- `2026-10-31T1412Z` = 2026-10-31 14:12 UTC.
- UTC only. No local time. The lab may be in any timezone; UTC is the only
  safe common reference.

## 3. Filename format

<CASE-ID><EVIDENCE-ID><TIMESTAMP>_<slug>.<ext> 

Examples:

SOC-001_EV-01_2026-10-31T1412Z_win-4625-discover.png
SOC-001_EV-02_2026-10-31T1415Z_win-4625-event-detail.png
SOC-001_EV-03_2026-10-31T1421Z_win-4624-after-failures.png
SOC-001_EV-04_2026-10-31T1430Z_linux-ssh-failures-authlog.log
SOC-001_EV-05_2026-10-31T1436Z_wazuh-alert-5710.json 

### Slug rules

- Lowercase only.
- Words separated by hyphens.
- Max ~40 characters.
- Describe **what the artifact shows**, not what tool made it.
  - Good: `win-4625-discover`, `linux-ssh-failures-authlog`
  - Bad: `screenshot1`, `image`, `final`, `new`

## 4. Folder structure per case

investigations/SOC-001-ssh-auth-failure-sim/

├── case.md

├── evidence-register.csv 

└── evidence/ 

├── screenshots/ 

│ ├── SOC-001_EV-01_....png 

│ └── SOC-001_EV-02_....png 

├── logs/ 

│ └── SOC-001_EV-04_....log 

└── exports/ 

└── SOC-001_EV-05_....json 


**Why case evidence lives inside the case folder, not in the global
`evidence/` folder:** each case must be self-contained and archivable. The
global `evidence/` folder holds lab-baseline proof and portfolio artifacts;
case evidence travels with its case. No duplication between the two.

## 5. Evidence register

Every case has an `evidence-register.csv` beside `case.md`. Every captured
artifact gets a row **before or at the moment of capture**.

Columns:

```csv
evidence_id,case_id,captured_utc,artifact_type,description,file_path,collected_by,linked_alert,linked_timeline_entry,sanitized
evidence_id,case_id,captured_utc,artifact_type,description,file_path,collected_by,linked_alert,linked_timeline_entry,sanitized
EV-01,SOC-001,2026-10-31T14:12Z,screenshot,Wazuh Discover view showing 4625 events,evidence/screenshots/SOC-001_EV-01_2026-10-31T1412Z_win-4625-discover.png,self,wazuh-rule-60122,TL-01,yes
EV-02,SOC-001,2026-10-31T14:15Z,screenshot,Event Viewer detail of one 4625,evidence/screenshots/SOC-001_EV-02_2026-10-31T1415Z_win-4625-event-detail.png,self,wazuh-rule-60122,TL-01,yes 
```
