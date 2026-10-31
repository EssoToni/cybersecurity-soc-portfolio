# Linux Telemetry Baseline Table — Analyst Questions

**Version:** 1.0  
**Date:** 2026-10-30  
**Scope:** Linux endpoint authentication, sudo, process and network telemetry as received by Wazuh.

> A log line tells what the system recorded. It does not, by itself, tell
> whether something malicious happened. Context turns telemetry into evidence.

## 1. Baseline table

| Event / Source | Source path | Meaning | Analyst question it answers | Key fields |
|---|---|---|---|---|
| **SSH authentication success** | `/var/log/auth.log` (`sshd`) | A user authenticated over SSH | *Is this login expected for this account, from this source, at this time?* | `user`, source IP, auth method (password / publickey) |
| **SSH authentication failure** | `/var/log/auth.log` (`sshd`) | A login attempt failed | *Is this user error, or brute force / password spraying?* | `user`, source IP, failure reason, attempt count |
| **sudo execution** | `/var/log/auth.log` (`sudo`) | A user escalated privileges | *Was this escalation authorized, and what command was run?* | `user`, `USER` (target), `TTY`, `PWD`, `COMMAND` |
| **sudo failure** | `/var/log/auth.log` (`sudo`) | A privilege escalation was denied | *Is a user probing for rights they do not have?* | `user`, `COMMAND`, reason |
| **Process execution (`EXECVE`)** | `/var/log/audit/audit.log` | A program was executed | *What ran, with what arguments, and under which UID?* | `comm`, `exe`, `key`, `uid`/`euid`, `success` |
| **User account change** | `/var/log/audit/audit.log` or `/var/log/auth.log` | An account was created, modified or deleted | *Was an identity changed that should not have been?* | `type` (`ADD_USER`, `USER_MGMT`), target account, `auid` |
| **Listening socket** | `ss -tulnp` (snapshot / command monitoring) | A service is listening on a port | *Is this port expected on this host?* | protocol, local address:port, process, user |
| **Established connection** | `ss -tanp` (snapshot / command monitoring) | An outbound or inbound connection exists | *Is this connection expected, and to where?* | local/remote address:port, process |

## 2. Event → Investigation question map

| If you see… | The first question to ask is… | Then pivot to… |
|---|---|---|
| Many SSH failures from one source | *Is this brute force?* | Source IP, targeted accounts, any subsequent SSH success |
| Sudo by an unexpected user | *Is this authorized escalation?* | `COMMAND`, `PWD`, preceding SSH login for that user |
| `EXECVE` with `comm` and `exe` from `/tmp` | *Is this execution legitimate?* | Parent process (via `ppid`), `uid`, subsequent network connections |
| A new listening port that was not in the baseline | *Is this an unauthorized service or backdoor?* | Process name, user, when it appeared |
| `USER_MGMT` record adding a user to a privileged group | *Is this persistence?* | Who made the change, which account, whether the actor was authorized |

## 3. What these sources do **not** prove

- An SSH success does not prove the account owner was present.
- A sudo line does not prove the command was malicious.
- An `EXECVE` record does not prove the binary was malware.
- A listening socket does not prove a backdoor.

**Context is the analyst's job.** The baseline is the reference point; the deviation from it is the signal.