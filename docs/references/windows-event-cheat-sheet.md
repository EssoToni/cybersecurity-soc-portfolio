# Windows Telemetry Cheat Sheet — Analyst Questions

**Version:** 1.0  
**Date:** 2026-10-29  
**Scope:** Windows Security log, core authentication, process and account-management events.

> An Event ID tells you what Windows recorded. It does not, by itself, tell you
> whether something malicious happened. Context turns telemetry into evidence.

## 1. Authentication — "Who logged in, how, and from where?"

| Event | What it records | Analyst question it answers | Key fields to read |
|---|---|---|---|
| **4624** | Successful logon | *Was this a legitimate logon, or a stolen credential?* | Logon Type (2=console, 3=network, 10=RDP), Account Name, Source Network Address, Authentication Package |
| **4625** | Failed logon | *Is this user error, or password spraying / brute force?* | Logon Type, Account Name, Failure Reason, Source Network Address, Status |
| **4634 / 4647** | Logoff / user-initiated logoff | *When did the session end?* | Account Name, Logon Type |
| **4648** | Logon with explicit credentials | *Did someone use RunAs or alternate credentials?* | Account Name, Target Server, Process |
| **4672** | Special privileges assigned | *Did an admin-level logon occur?* | Account Name, Privileges |

### Logon Type quick reference

| Type | Meaning |
|---|---|
| 2 | Console (someone at the keyboard) |
| 3 | Network (share, service-to-service) |
| 4 | Batch (scheduled task) |
| 5 | Service |
| 7 | Screen unlock |
| 10 | Remote Interactive (RDP) |
| 11 | Cached credentials (offline logon) |

## 2. Process execution — "What ran, and who launched it?"

| Event | What it records | Analyst question it answers | Key fields to read |
|---|---|---|---|
| **4688** | Process created | *What executable started, and what is its parent?* | New Process Name, Creator Process Name, Command Line (if enabled), Subject Account Name |
| **4689** | Process exited | *How long did the process run?* (Pair with 4688 to bound lifetime) | Process Name, Exit Status |

> **Prerequisite:** 4688 only includes the command line when "Include command line in process creation events" is enabled via Group Policy. Without it, 4688 is a fraction as useful.

### Parent–child reasoning examples

- `explorer.exe` → `cmd.exe` = normal user action.
- `winword.exe` → `powershell.exe` = macro execution; investigate.
- `services.exe` → `cmd.exe` = suspicious; services should not spawn shells.

## 3. Account management — "Was an identity created, changed, or abused?"

| Event | What it records | Analyst question it answers |
|---|---|---|
| **4720** | User account created | *Was an account created that should not exist?* (Common persistence.) |
| **4722** | User account enabled | *Was a disabled account reactivated?* |
| **4724** | Password reset attempted | *Who reset whose password, and was it authorized?* |
| **4725** | User account disabled | *Was an account disabled unexpectedly?* |
| **4726** | User account deleted | *Was an account removed?* (Anti-forensics or cleanup.) |
| **4738** | User account changed | *What changed?* (Group membership, UPN, permissions.) |
| **4740** | User account locked out | *Brute force, or user error?* (Pair with 4625.) |

## 4. Event ID → Investigation question map

| If you see… | The first question to ask is… | Then pivot to… |
|---|---|---|
| **4625** repeated for many accounts from one source | *Is this password spraying?* | Source IP, account list, 4624 successes after the failures |
| **4624 Type 10** from an unexpected host | *Is this unauthorized RDP?* | Source host, account, preceding 4625s, 4688 on the source |
| **4688** with a parent–child pair that does not match normal | *Is this execution chain legitimate?* | Command line, user context, file hash (Sysmon), network connections |
| **4720** followed by **4732** (group add) | *Is this account-creation-then-promotion persistence?* | Who created it, what group, whether the creator was authorized |
| **4740** for a service account | *Is a service failing, or is this a brute-force side effect?* | 4625 count, source addresses, whether the service is still healthy |

## 5. What these events do **not** prove

- 4624 does not prove the account owner was present.
- 4625 does not prove an attack occurred.
- 4688 does not prove malware ran.
- 4720 does not prove malice — it proves an account was created.

**Context is the analyst's job.** Event IDs are the starting point, not the conclusion.