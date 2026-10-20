# Task 3 – Response playbook and evidence preservation (25 marks)


**Stage:** Containment, Eradication and Recovery, with evidence handling from Detection and Analysis (ICDFA, n.d., slides 10–11). Method: contain first to stop harm, but preserve what I can before each change. The CISA guide supports isolating affected systems while preserving volatile evidence, treating power-off as a last resort, using out-of-band communication, and checking backups for malware before restoration (CISA et al., 2023). All times are WAT on Day 0 (Monday) unless stated. Every action below is a **plan**; none has been performed.


## 3.1 Response playbook


*Table 10. Ordered playbook for the first 60 minutes (steps 1–9) and the remainder of the first 24 hours (steps 10–19). Evidence IDs refer to Table 11.*


| **Step / time / stage** | **Action** | **Owner** | **Required approval** | **Evidence to retain** | **Completion check** |
|---|---|---|---|---|---|
| 1<br>08:45–08:50<br>Declare | Declare a **Critical** incident. Open the incident log and decision log. Start a written clock. Assign roles. Treat corporate email as untrusted (E08). | IRL (Scribe logs) | Pre-delegated authority (A2). Executive Sponsor informed by phone. | Incident log entry; time of declaration; role assignment. | Log opened with time stamp. Roles confirmed by phone. |
| 2<br>08:50–09:00<br>Communicate | Phone the core CSIRT and the Executive Sponsor. Open an out-of-band conference bridge by voice call. Use staff mobiles (E08, A8). Tell helpdesk to reroute learner queries to a holding script. | IRL; COM | None (Critical trigger). | Call log with times and attendees. | All core roles reached or an alternate named. |
| 3<br>08:55–09:05<br>Short-term containment | Isolate **FS01**: block its network port or VLAN, or disable its NIC. Do **not** power off. Screenshot the ransom note and sample .locked files first. Isolate **FIN-PC07** using EDR network containment, keeping it powered. | ITO (SA for EDR) | IRL (delegated). | Photographs of the ransom note. EDR isolation record. Switch or hypervisor change record with time. Planned EV-01, EV-03. | Pings from the user network to FS01 and FIN-PC07 fail. EDR shows host isolated. |
| 4<br>09:00–09:10<br>Protect backups | Disable **svc_backup** everywhere. Disconnect **BAK01** from the network, or block its SMB and management ports. Suspend backup jobs and retention or expiry deletion. Locate and physically secure the **Friday 17:00** disconnected backup. | ITO | IRL. | Account audit log. BAK01 configuration export. Photograph of the secured media. Planned EV-05, EV-07. | svc_backup shows disabled. No inbound connection to BAK01 from any host. Media location confirmed. |
| 5<br>09:05–09:20<br>Identity containment | Export M365 sign-in and audit logs **first**, then revoke all sessions and tokens for the finance officer, reset password, require MFA re-registration, and block the unfamiliar IP and device. Review inbox rules, forwarding, OAuth app consents and MFA methods. Reset passwords for privileged M365 and local admin accounts. | ITO; SA | IRL. | Exported logs (EV-04). Screenshots of rules and consents found. | Revocation confirmed in the audit log. No unknown rules, consents or MFA methods remain. |
| 6<br>09:10–09:20<br>Suspicious transfer | Block the destination of the 1.2 GB upload at the proxy and firewall. Preserve proxy logs. Ask counsel to prepare a preservation or takedown request to the cloud provider. | SA; LEG | IRL; LEG for the provider request. | Proxy log export (EV-06). Destination domain and IP. | Block rule active. Further attempts to reach the destination are seen in logs. |
| 7<br>09:15–09:30<br>Volatile evidence | Where safely achievable within about 15 minutes, take memory and a triage collection from FIN-PC07 and FS01, using the EDR or a trusted tool. Do not install new tools on FS01 beyond the minimal capture agent. If external DFIR is not on site, SA collects what can be collected and records what is lost. | SA (FOR guides remotely) | IRL; FOR if available. | Planned EV-02, EV-03. Evidence-loss note for anything not captured. | Collection recorded in the register with planned hash step. Loss note written if skipped. |
| 8<br>09:30<br>Brief and escalate | Brief the Executive Sponsor in writing (Task 4). Engage external DFIR and legal counsel. Start the 72-hour regulatory clock record (Task 4) as a precaution. | IRL; EXEC | EXEC approves external engagement and spending. | Executive briefing as sent. Time of DFIR and counsel call. | DFIR and counsel confirm availability and arrival time. |
| 9<br>09:45<br>Exam and portal | Take a read-only snapshot of LMS01. Assess whether LMS01 itself is clean (Q4). Prepare the examination go/no-go criteria for 10:00 (Decision 2). | ITO; SA | BO decides at 10:00. | LMS01 snapshot reference. Integrity check results. | Go/no-go criteria sheet complete. Decision recorded. |
| 10<br>10:00–10:15<br>Decision gate | Examination go/no-go. Default: **postpone** unless every criterion in Decision 2 is met. Send learner notice by 10:15 (Task 4). | BO (A); IRL (R) | BO with EXEC informed. | Decision record and rationale. Notice as sent. | Learners informed by 10:15. Decision log updated. |
| 11<br>10:15–12:00<br>Scope sweep | Sweep for indicators of compromise from FIN-PC07 on every workstation using EDR. Triage all servers manually, since EDR coverage is incomplete. Check for new local admins, scheduled tasks, remote-access tools and unknown services. Review proxy logs for other transfers. Search for the ransom note and .locked files on every share. | SA; ITO | IRL. | Sweep query and results. List of hosts checked and unchecked. | Every host marked clean, suspect or not checked. Uncovered hosts have a named owner. |
| 12<br>10:15–13:00<br>Investigate | Analyse the entry vector (Q1): message trace, attachment sample in an isolated sandbox, EDR process tree. Analyse svc_backup (Q2) and the upload (Q3). Identify the ransomware family from the note and a sample, with no ransom-contact or payment step without counsel and the Executive Sponsor. | FOR; SA | IRL. | Sandbox report. Logon analysis. Timeline updates. Planned EV-08. | Q1–Q3 each have a written finding or a stated blocker. |
| 13<br>12:00–15:00<br>Backup validation | Select and validate a backup (3.4). Restore a copy into an **isolated** environment. Scan, compare integrity and test application function. | ITO; FOR | IRL; BO informed. | Restore log. Scan results. Integrity report. | Backup meets acceptance criterion 1 (3.5), or is rejected in writing. |
| 14<br>13:00–17:00<br>Longer-term containment | Rotate all privileged and service credentials. Apply conditional access and MFA for admins. Segment LMS01, BAK01 and FS01 so that one admin path cannot reach all. Block newly seen indicators. Extend EDR to servers where feasible. | ITO; SA | IRL. | Change records. Rotated account list. | No old credential still works. Segmentation tested. |
| 15<br>15:00–Day 1 06:00<br>Eradication | Rebuild FIN-PC07 and FS01 from known-good images, not cleaned in place. Remove persistence found in step 11. Patch the exploited weakness. Confirm that the mail filter now blocks the attachment type or sender. | ITO; FOR confirms | IRL; BO informed. | Rebuild records. List of persistence removed. | Rebuilt hosts pass malware scans. No indicators remain after rescan. |
| 16<br>17:00–21:00<br>Briefings | Update executives (every 2 hours), staff, and learners. Review the attacker’s claim and threat deadline with counsel. No public statement on data unless approved by LEG and EXEC. | COM; IRL | EXEC and LEG. | Notices as sent. Log of attacker contact (if any). | Updates sent on schedule. |
| 17<br>Day 1 06:00–14:00<br>Recovery | Restore in the agreed order (3.4) into a segmented network. Check integrity of restored data (hash lists, sample opens, application tests). Run enhanced monitoring. | ITO; SA | BO (A) for each service return. | Restore logs. Integrity test records. | Each service meets its acceptance criteria before release. |
| 18<br>Day 1–Day 7<br>Monitoring | Enhanced monitoring for 7 days. Re-check for persistence, new sign-ins, mail rules and uploads. Daily stand-up. | SA | IRL. | Daily monitoring report. | No unexplained indicator for 7 consecutive days. |
| 19<br>Day 1<br>Closure of operations | Hand off from incident mode to normal operations when acceptance criteria are met. Close the evidence register with custody records. Schedule review. | IRL; EXEC | EXEC (A). | Closure memo. Final register. | All register items have custody to date. Review meeting scheduled. |


That is 19 ordered actions: nine in the first hour of the clock (08:45–09:45), and ten for the rest of the first 24 hours (steps 10–19; steps 18–19 extend to the first week).


### How I will check for broader compromise


- **Hosts:** EDR indicator sweep across all workstations, and manual triage of all servers where EDR is missing, using hashes, filenames, persistence locations and network indicators from the first hosts.
- **Accounts and cloud:** review M365 sign-ins from the unfamiliar IP or device for every user (not only the finance officer), inbox rules, forwarding, OAuth consents, newly registered MFA methods and mailbox permissions.
- **Privileged paths:** every system where svc_backup or any admin account logged on in the last 30 days; any new accounts or group changes.
- **Network and data:** proxy, DNS and firewall logs for large outbound transfers or beaconing in the 14 days before E01 and since, including repeat contact to the E04 destination.
- **Third parties:** confirm with the backup, cloud and email providers that they see no unusual activity in their own logs.

Limits: with incomplete server EDR coverage and no known log retention period (**unresolved**), a clean sweep reduces risk but does not prove absence of compromise. That limit is stated in every briefing.


## 3.2 Two difficult decisions


### Decision 1 – Containing while preserving useful evidence


**Decision:** Isolate FS01 and FIN-PC07 from the network immediately and leave both powered on. Capture volatile data only if it can be done within about 15 minutes without delaying isolation of FS01.


**Rationale.** Mass file changes were seen at 08:30 (E06), so encryption may still be spreading to other shares, and BAK01 is reachable by an account the attacker may control (E03). Each extra minute risks more data lost, and loss of the backups would remove my main recovery option. Memory and running-process data is useful for finding the encryption key material, the attacker’s tools and persistence, but it is lost on shutdown, so I avoid powering off (CISA et al., 2023). Network isolation stops spread and keeps memory. The slide deck makes the same sequence explicit: isolate, then preserve before further change (ICDFA, n.d., slide 11).


**When immediate isolation, with no evidence capture first, is necessary.** (a) Encryption is visibly spreading to new hosts or shares. (b) BAK01 or backup media show signs of active access, deletion or encryption. (c) Data is currently leaving the network. (d) The attacker is interactively active. Any one of these overrides evidence capture. At 08:45 (a) and (b) are possible and so I isolate first and capture second.


**How evidence loss and impact are documented.** The Scribe records for each action the time, the person, the reason, what was and was not captured, and the business impact (for example, finance staff cannot work and FS01 shares are offline). Anything not captured is entered in an **evidence-loss note** and given to the forensic provider and counsel, so that an investigator or regulator can see that the loss was a deliberate, reasoned trade-off. This is an operational impact that the Executive Sponsor is told about in the 09:30 briefing.


### Decision 2 – Restoring examination access while backup safety is uncertain


**Options considered.**


| **Option** | **Benefit** | **Risk** | **Verdict** |
|---|---|---|---|
| A. Reopen the portal on current FS01 and LMS01 and run the 11:00 examination. | Meets the deadline. | Serves content from an encrypted or compromised server. Risks reinfection, corrupt results, learner data exposure, and loss of evidence. | Rejected. |
| B. Restore LMS01 content from the Friday 17:00 disconnected backup into a clean, isolated environment and run the examination. | Uses the most trustworthy backup (A7), and keeps the exam. | Needs identity reset, validation and testing in about 75 minutes, and submissions have no safe place to land if FS01 is down. Backup not yet tested (Q2). | Only if all five gate criteria are met by 10:00. |
| C. Postpone the examination and give learners a new date. | Safe. Fully reversible. Time for validation. | Disruption to 100 learners. Reputational cost. Possible institutional or accreditation rules on assessment dates (**unresolved**). | Default. |


**Decision:** Hold a go/no-go gate at **10:00**. Postpone (Option C) unless **all** of these are true: (1) LMS01 is shown clean by snapshot scan and integrity comparison; (2) content is restored from a validated backup into an isolated segment, not on the compromised FS01; (3) the M365 accounts of the 100 learners and examiners are not in scope of the compromise and the finance session revocation is complete; (4) a safe place exists for submissions, with a plan for recovering them; (5) the Business Owner accepts the residual risk in writing. If any criterion fails, we postpone and tell learners by 10:15.


**Rationale.** Delay is recoverable, but corrupted assessment records, reinfected systems and exposed learner data are not. A false restoration also risks the integrity of the very recovery path that all other services depend on. This is a business risk decision, and so the Business Owner (A) makes it with advice from me (R), as in the RACI (Table 8). The decision log records the data loss (work since Friday 17:00) and the operational impact of postponement.


## 3.3 Evidence register and custody arrangements


**Status of every item is “planned / not yet collected”.** I have not performed any acquisition, and the register contains no hash values. Integrity values are to be computed at the time of collection and recorded then. Dates and times are targets in WAT (UTC+1).


*Table 11. Evidence register (planned). CoC = chain of custody form.*


| **ID** | **Source** | **Proposed collection method** | **Collector role** | **Date and time (WAT)** | **Integrity check** | **Secure storage** | **Custody transfers** |
|---|---|---|---|---|---|---|---|
| EV-01 | FIN-PC07 disk and EDR telemetry (E01, E04, E06) | EDR triage package and, if DFIR agrees, forensic disk image taken via write-blocked or approved tool after isolation. | SA, then FOR | Not yet collected. Target Day 0 10:00–14:00. | SHA-256 of image and package, to be computed at acquisition and recorded on the CoC. | Encrypted external drive in evidence safe. Working copy on separate analysis system. | To be recorded on CoC-01: SA → Scribe → FOR. |
| EV-02 | FIN-PC07 memory | Memory capture with approved tool before any reboot. | SA | Not yet collected. Target Day 0 09:15–09:30. | SHA-256 at capture. Tool and version recorded. | As EV-01. | CoC-02: SA → Scribe → FOR. |
| EV-03 | FS01: memory, triage collection, ransom note, sample .locked files, event logs | Minimal-footprint triage collector. Photograph the note and file names. Export event logs. Full image later by FOR. | SA, then FOR | Not yet collected. Target Day 0 09:15–09:45 (triage), image by 14:00. | SHA-256 of each file or container at collection. | As EV-01. Separate container per host. | CoC-03: SA → Scribe → FOR. |
| EV-04 | M365 audit, sign-in and mailbox logs for finance officer and all users (E02) | Export via admin portal or API before any revocation, under a named administrator account with MFA. | ITO under SA supervision | Not yet collected. Target Day 0 09:00–09:15. | SHA-256 of exported files. Export query and time recorded. | Encrypted evidence store, offline copy. | CoC-04: ITO → Scribe → FOR. |
| EV-05 | Windows Security logs from FS01 and BAK01, svc_backup activity (E03) | Export .evtx files and event query results. | ITO | Not yet collected. Target Day 0 09:10–09:30. | SHA-256 at export. | As EV-04. | CoC-05: ITO → Scribe → FOR. |
| EV-06 | Proxy and firewall logs, 1.2 GB upload (E04) | Export the full log slice for the 14 days before E01 to the present. | SA | Not yet collected. Target Day 0 09:15–09:40. | SHA-256 of exports. | As EV-04. | CoC-06: SA → Scribe → FOR. |
| EV-07 | BAK01 configuration, job catalogue, retention settings, and Friday 17:00 disconnected media (E05) | Export configuration after network isolation. Photograph and seal the Friday media. Do not mount it on a production host. | ITO; Scribe seals | Not yet collected. Target Day 0 09:10–09:30. | SHA-256 of exports. Media serial number and seal number recorded. | Sealed media in safe, signed in and out. | CoC-07: ITO → Scribe → FOR. |
| EV-08 | Original phishing email and attachment (E01) | Export the message as .eml with headers from the mail platform. Handle the attachment only in a sandbox. | SA | Not yet collected. Target Day 0 10:15–11:00. | SHA-256 of .eml and attachment. | Encrypted evidence store, offline. | CoC-08: SA → Scribe → FOR. |


**Access restrictions and custody rules.** (1) Only the Scribe/Custodian, the IRL and the forensic provider can open the evidence store. (2) Evidence is held on encrypted media kept off the compromised domain, with an offline copy. (3) Originals are never examined directly, and only working copies are analysed. (4) Every transfer is recorded on the chain-of-custody form with date, time (WAT), from, to, purpose and hash re-check. (5) Anyone taking evidence signs it out and back in. (6) Hash values are written down at collection by the collector and verified by a second person at transfer (ICDFA, n.d., slides 7 and 10). (7) Counsel is told what is collected, so privilege and disclosure can be managed.


## 3.4 Eradication, credentials and recovery


### Persistence removal, entry point and credentials


- **Persistence.** Treat every host in scope as untrusted. Rebuild FIN-PC07 and FS01 from known-good images instead of cleaning them. For other hosts with indicators, remove scheduled tasks, services, registry run keys, startup items, unknown remote-access tools and new local accounts, then re-scan with more than one tool and re-check after 24 hours (ICDFA, n.d., slide 11).
- **Entry point.** The likely vector is the payroll attachment (E01, **hypothesis**). I will confirm it by message trace and sandbox analysis, remove the message from all mailboxes, block the sender and file type, and check for any other recipients. I will keep an open mind about alternatives (an exposed remote service or a stolen credential) until the evidence rules them out.
- **Credentials.** Reset the finance officer’s password and sessions and re-register MFA. Rotate svc_backup, all administrator, break-glass and service credentials, and API keys, and issue them from a clean device. Revoke OAuth consents and unknown MFA methods. Require MFA for all admins. Do not reuse svc_backup. Create a replacement with least privilege and no standing admin reach across FS01 and BAK01.

### Recovery order and targets


*Table 12. Recommended restoration order and targets. RTO and RPO are my proposals for approval by the Business Owner, because the brief gives none.*


| **Order** | **Service** | **Why this order** | **Target: restored by** | **Acceptable data loss (RPO)** |
|---|---|---|---|---|
| 1 | Identity and email hygiene (M365 clean-up, alternative channel) | Everything else depends on trusted identity and communications. | Day 0 by 12:00 | None (cloud service; settings only). |
| 2 | FS01 content needed by the portal, restored into an isolated segment | The portal depends on FS01 files (A6). | Day 1 by 10:00 | Up to Friday 17:00 (about 63 hours 45 minutes). Work since then is re-created or re-submitted (A9). |
| 3 | LMS01 learning portal and examination service | Business-critical. Needed for the examination re-run. | Day 1 by 14:00, subject to Decision 2 criteria | As FS01. |
| 4 | FS01 general shares | Needed by staff, but lower than teaching. | Day 2 | As FS01. |
| 5 | FIN-PC07 and finance files | Rebuild first, then restore data after checks. Finance is sensitive and subject to scrutiny. | Day 2–3 | As FS01, with reconciliation by finance. |
| 6 | BAK01 rebuild with immutable or offline copy | No new backups are safe until the repository is rebuilt. | Day 2–3 | n/a |


*The Friday 17:00 to Monday 08:45 gap is 63 hours 45 minutes. Any later network backup is used only if validated as clean (A7, A9).*


### Selecting and validating a backup


1. **Candidate selection.** List all restore points: the Friday 17:00 disconnected backup and the network backups (including the 02:00 jobs in E05). Choose the **most recent point before the earliest evidence of compromise** (E01, Sunday 16:40, plus margin for unknown dwell). The Friday disconnected copy is the default. Any later network copy is a candidate only if it passes all checks.
2. **Provenance.** Confirm the media or snapshot was not mounted on a compromised host since Friday (EV-07), and compare job logs, catalogue and timestamps with BAK01 activity from E03.
3. **Isolated test restore.** Restore into an isolated network with no route to production, using new credentials.
4. **Malware and integrity checks.** Scan with more than one tool, search for ransom-note files, .locked extensions, known indicators and unexpected binaries. Compare file counts, sizes and hashes of a sample with known-good data (for example, vendor packages for LMS01). Check that files open and databases mount.
5. **Controlled production restore.** Restore to rebuilt systems on a segmented network with only the access needed. Keep the isolated copy for evidence.
6. **Monitoring before approval.** Run the restored service under enhanced monitoring, then present results to the Business Owner.

## 3.5 Recovery acceptance criteria


The Business Owner may approve return of a service only when **all** of the following are met and recorded:


1. The backup used was validated (provenance, isolated restore, scans and integrity tests all passed and documented).
2. The host or service runs on a rebuilt or verified-clean platform, and sweep results show no indicators of compromise on it.
3. All credentials that could reach the service were rotated, and no old credential works. MFA is enforced for admin and finance access.
4. The entry point is identified and fixed or mitigated, or an explicit compensating control is accepted by the Executive Sponsor.
5. Application tests pass (login, content access, submission and results retrieval, for the portal) with sample data checked against known values.
6. Enhanced monitoring is live, with alerting for the indicators found, and no unexplained alert for at least 24 hours before return and 7 days after.
7. Data loss against RPO is documented and accepted in writing, and affected users know what must be re-created.
8. Evidence has been captured and custody records are up to date, so rebuilds do not destroy needed evidence.
9. Rollback is defined: if a new indicator appears, the service is isolated again.

---

[⬅ Back to README](../README.md) | [⬅ Previous: Task 2 – Incident response plan and team responsibilities (20 marks)](02-task2-ir-plan-and-raci.md) | [Next: Task 4 – Communication and escalation (10 marks) ➡](04-task4-communication-and-escalation.md)
