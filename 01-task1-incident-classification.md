# Task 1 – Incident classification and initial assessment (15 marks)


**Stage:** Detection and Analysis (ICDFA, n.d., slides 9–10). Clock: 08:45 WAT, Monday, Day 0, when I take control. The 11:00 examination for 100 learners is 2 hours 15 minutes away.


## 1.1 Evidence-linked timeline


*Table 1. Timeline of E01–E08 separating what is confirmed from what is hypothesised and unresolved. Times are WAT.*


| **Time** | **ID** | **Confirmed observation** | **Working hypothesis** | **Unresolved question** |
|---|---|---|---|---|
| Fri, Day −3 17:00 | Brief | Last disconnected backup completed. Network backups are not immutable. No restoration test on either route in 90 days. | Predates the intrusion (A7). | Is it complete and restorable? |
| Sun, Day −1 16:40 | E01 | Finance officer reports opening an unexpected payroll attachment on FIN-PC07 (user report and mail record). | Phishing attachment was the initial access vector. | Did the code execute? What was the file? Which sender and which other recipients? |
| Mon, Day 0 01:15 | E02 | M365 audit shows a sign-in to the finance officer account from an unfamiliar IP and new device. | Credentials or session token stolen after E01. | Was MFA used, bypassed or absent? Was it the user? |
| 01:35 | E03 | svc_backup made remote administrator logons to FS01 and BAK01 outside its usual schedule. | Attacker used svc_backup to move laterally and reach the backups. | Reason? Source host or IP? Was it a change or maintenance task? |
| 01:50 | E04 | Proxy shows FIN-PC07 uploaded 1.2 GB over HTTPS to unfamiliar cloud storage. | Possible staging and exfiltration of data before encryption. | What was in the 1.2 GB? Did it contain personal data? Was it a legitimate sync? |
| 02:00 | E05 | Backup console shows FS01 and LMS01 jobs as successful. | Jobs ran, but the data may be encrypted, tampered or already compromised. | Is the backup readable and clean? Can BAK01 be trusted after E03? |
| 08:30 | E06 | EDR and helpdesk report mass file changes on FIN-PC07. FS01 shares contain .locked files and a ransom note. | Ransomware encryption is active or has just completed. Family unknown. | Which family? When did encryption start on FS01? Other hosts affected? |
| 08:40 | E07 | Portal login page loads, but learners cannot open materials or submit assessments. | LMS01 is degraded because it depends on FS01 files (A6), not necessarily itself compromised. | Is LMS01 itself encrypted, altered or clean? |
| 08:45 | E08 | Incident contact list on FS01 is inaccessible. Staff phones work. | The list was encrypted with the share. | Is corporate email trustworthy? Are attacker rules or forwarding in place? |


**Reading across the timeline.** E02–E05 fall inside a 45-minute window (01:15–02:00) in the middle of the night, and E06 follows about six and a half hours later. That pattern is consistent with a staged attack (access, privilege use, data staging, backup interference, then encryption), but it is a **hypothesis**. I have no evidence for the 02:00–08:30 interval, which is a visibility gap to be closed from log retention.


### Plausible alternative explanations for ambiguous events


| **Event** | **Leading hypothesis** | **Alternative explanation** | **Check that separates them** |
|---|---|---|---|
| E02 – unfamiliar sign-in | Attacker with stolen credentials or an adversary-in-the-middle session token. | (a) The officer legitimately signed in from a new phone or network, for example while travelling or on mobile data. (b) A password-spray or sign-in attempt that failed MFA and never succeeded. | Sign-in log result codes, MFA method used, token issuance, device ID, and a short interview with the officer. |
| E03 – svc_backup logons | Attacker reused the service account to reach FS01 and BAK01. | (a) A scheduled change, patch or vendor maintenance job ran off-schedule. (b) A backup job re-run after a failed run. | Source IP and logon type in Windows Security events, change tickets, and IT team confirmation. |
| E04 – 1.2 GB upload | Exfiltration of finance or learner data. | (a) A legitimate cloud sync or personal backup of large files. (b) Malware beaconing or tool download with little sensitive content. | Destination ownership, full proxy URL and SNI, EDR file-read telemetry, FS01 file-access audit, and timing against E02. |
| E05 – backup success | Backups are usable. | Jobs report success even when they back up already-encrypted or tampered data. Success means the job ran, not that the data is recoverable. | Test restore into an isolated environment, and compare file hashes and entropy against known-good data. |


## 1.2 Incident classification and severity


**Classification.** Ransomware (encryption with extortion note), with **suspected** data exfiltration (double extortion), **suspected** compromise of one user account and one privileged service account, and **suspected** interference with backups. Initial attack vector: phishing attachment (**hypothesis**, E01). Attribution to any named group is not established, and I will not assert it. The slide deck rates ransomware as Critical (ICDFA, n.d., slide 4).


*Table 2. Severity criteria used in this plan (adapted from the Critical, High and Medium/Low tiers on slide 10; I added the Low tier).*


| **Level** | **Criteria (any one is enough unless stated)** | **Response expected** |
|---|---|---|
| **Critical** | Confirmed or likely loss of availability or integrity of a critical service or data set with a hard deadline; or likely exposure of personal data; or doubt about the integrity of the recovery source; or active spread to new systems. | Immediate full CSIRT activation. Executive notified within 15 minutes. Legal and privacy advice engaged. External DFIR engaged. |
| **High** | Confirmed compromise of one non-critical system or a single account, no sign of data exposure, backups verified safe, impact contained within hours. | Rapid response within SLA. Management notified. Core CSIRT on call. |
| **Medium** | Malware or policy violation on a single endpoint, contained, no sensitive data involved, no service impact beyond that user. | Standard workflow, ticketed and tracked. |
| **Low** | Blocked or failed attempt, or a suspicious event with no evidence of compromise. | Logged and monitored. Reviewed in routine meeting. |


**Selected level: CRITICAL (provisional), declared at 08:45.** Justification:


- **Operational impact (confirmed).** Encryption on FIN-PC07 and FS01 (E06) and learner access to materials and submissions failing (E07). A 100-learner examination starts in 2 hours 15 minutes, and the contact list is unavailable (E08).
- **Affected data (potential).** FS01 holds data that the brief says the institute keeps (learner contact details, admission documents, assessment records, finance files). A 1.2 GB upload (E04) and the ransom note make exfiltration plausible, but it is **unproven**.
- **Uncertainty.** An off-schedule privileged account (E03) and unverified backups (E05) mean the recovery source may be compromised. I rate on the **credible worst case** until evidence reduces it, as the response cost of over-rating for a few hours is far lower than that of under-rating.
- **What would lower or raise the rating.** I would move to High if: encryption is confirmed limited to FIN-PC07 and FS01, LMS01 is verified clean, BAK01 and the Friday backup are verified untouched, and logs show E04 was not personal data. The rating stays Critical, and the regulator and notification workstream escalates, if personal data exfiltration is confirmed or backups are found tampered.

## 1.3 Affected assets and CIA impact


*Table 3. Assets, status and separate confidentiality, integrity and availability (C, I, A) assessment. Status key: Confirmed = affected per evidence; Potential = at risk but unproven.*


| **Asset** | **Status (evidence)** | **Confidentiality** | **Integrity** | **Availability** |
|---|---|---|---|---|
| FIN-PC07 finance workstation | Confirmed – E01, E04, E06 | High risk: payroll and finance data, 1.2 GB upload (E04). | Compromised: mass file changes (E06). | Lost for the officer. |
| FS01 shared file server | Confirmed – E06 | Possible: privileged access seen (E03). | Compromised: .locked files and ransom note. | Lost for all users and for LMS01 content. |
| LMS01 learning portal | Potential – E07 | Unknown. Content and learner records may be exposed. | Unknown. Needs file-integrity check. | Degraded: login loads but materials and submissions fail. |
| BAK01 backup repository | Potential – E03, E05 | Possible: holds copies of all data. | Not trusted until verified; may be altered or deleted. | Unknown. Online and not immutable. |
| Finance officer M365 account / mailbox | Potential – E01, E02 | High risk: mail, OneDrive and shared data. | Possible rule or forwarding changes. | Available to attacker, to be disabled. |
| svc_backup account | Potential – E03 | Admin access to FS01 and BAK01. | Used outside its schedule. | Must be disabled, which may stop backups. |
| Incident contact list | Confirmed – E08 | n/a | n/a | Lost: it was on the encrypted server. |
| Examination service (100 learners, 11:00) | Confirmed at risk – E07 | Assessment content and answers may be exposed. | Risk of corrupted or untrusted results. | At risk of failing to run. |


### Response priorities (in order)


1. **Stop spread and protect recovery options.** Isolate FIN-PC07 and FS01, suspend svc_backup, and cut BAK01 off the network. Justification: E03 and E05 mean the backups are the asset the attacker most likely wants to deny me.
2. **Preserve evidence while containing.** Capture volatile data and logs before they are lost, and record every action with a timestamp (ICDFA, n.d., slide 11: preserve forensic evidence before changes are made).
3. **Contain the identity layer.** Revoke sessions and reset the finance account, because the attacker may still have M365 access (E02).
4. **Decide the examination by 10:00.** Give a go/no-go decision with enough time to tell learners, and do not reopen the portal on unverified storage.
5. **Establish out-of-band communication.** Use phones (E08) while email trust is unverified.
6. **Scope and validate.** Find the entry point and exfiltration, and validate a backup before any restoration.

## 1.4 Priority investigation questions


*Table 4. Priority investigation questions, resolving checks, and how findings would change severity or scope.*


| **#** | **Question** | **Resolving check (planned)** | **Finding that changes severity or scope** |
|---|---|---|---|
| Q1 | Did the attachment execute on FIN-PC07, and is the finance account compromised (E01, E02)? | Message trace and headers for the payroll email. EDR process tree on FIN-PC07. M365 sign-in logs (result, MFA, device, token). Interview the officer. | If the account is compromised, then M365 mail, OneDrive and SharePoint enter scope and email is untrusted (affects all communications). If the sign-in was the user, the scope narrows to the endpoint. |
| Q2 | Was svc_backup misused, and has BAK01 or its backup data been altered or deleted (E03, E05)? | Windows Security events (logon type, source IP) on FS01 and BAK01. Change tickets. Interview IT. BAK01 job catalogue, retention and deletion logs. Test restore in isolation. | If tampering is found, the recovery source becomes the Friday disconnected backup, recovery time lengthens and data loss rises. If benign, restoration from network backup may be faster. |
| Q3 | What was in the 1.2 GB upload, and did it include personal data (E04)? | Full proxy log (URL, SNI, bytes). DNS and firewall flow records. EDR file-read telemetry. FS01 file-access audit. Cloud provider ownership lookup. | Personal data confirmed means formal notification workstream starts at once (Task 4) and the learners are informed. A legitimate sync would lower this risk. |
| Q4 | Is LMS01 itself compromised, or only starved of FS01 files (E07)? | Read-only snapshot of LMS01. File integrity comparison against vendor package. Application and web logs. Manual malware scan, since server EDR is incomplete. | If clean, a controlled restore of FS01 content could allow a limited portal return. If compromised, the portal cannot return until rebuilt. |
| Q5 | Has the attacker reached other systems or established persistence beyond FIN-PC07 and FS01? | EDR indicator sweep on all workstations. Manual triage of servers. M365 inbox rules, OAuth app consents and registered MFA methods. Scheduled tasks and new local admins. | Additional hosts or persistence expand eradication scope and delay any restoration approval. |

---

[⬅ Back to README](../README.md) | [⬅ Previous: Reading guide and assumptions](00-assumptions-and-reading-guide.md) | [Next: Task 2 – Incident response plan and team responsibilities (20 marks) ➡](02-task2-ir-plan-and-raci.md)
