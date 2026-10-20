# Task 5 – Tabletop exercise and improvement plan (15 marks)


> **SIMULATION NOTICE.** Everything in this task is a **simulated, fictional exercise** that I ran alone on paper, playing each role in turn. No real system, person or regulator was involved. The “results” are my reasoned simulation and are not observations from a real incident. The exercise tests the plan from Tasks 1–4 (ICDFA, n.d., slides 8 and 18).


## 5.1 Exercise design


### Objectives


1. Test whether the declaration, authority-to-isolate and containment sequence in the playbook works within the target times.
2. Test the examination go/no-go gate under management pressure to reopen the portal.
3. Test backup selection and validation, including what happens when a backup fails.
4. Test communication discipline under pressure: attacker claim, social media and a journalist.
5. Test the decision log and the evidence register as working tools.

### Participant roles


Each role below is played by me in turn, speaking from that role’s responsibilities in Table 7 and Table 8: Incident Response Lead (IRL, facilitator), Security Analyst (SA), Forensics Lead (FOR), IT Operations Lead (ITO), Business Owner (BO), Legal and Privacy Adviser (LEG), Communications Lead (COM), Executive Sponsor (EXEC) and Scribe (SCR). In a live version, each role is played by its holder and I would act only as facilitator (assumption A10: minute 0 = 08:45 WAT on Day 0).


### Agenda (60 minutes)


| **Minute (clock)** | **Activity** |
|---|---|
| **0–10 (08:45–08:55)** | Scenario brief. Roles confirmed. Declaration, first containment and communication steps (playbook steps 1–5). |
| **10 (08:55)** | **Inject 1** – Management asks to reopen the portal before 11:00, even with an unverified backup. Discussion and decision. |
| **20 (09:05)** | **Inject 2** – Attacker claims to hold all 1,800 learner records, threatens publication in 12 hours (deadline 21:05), and supplies a screenshot of unknown authenticity. |
| **28 (09:13)** | **Inject 3 (my own)** – Alert: a new inbox rule and an OAuth consent appear on the finance account, and a sign-in to a senior manager’s mailbox from the same unfamiliar IP. |
| **35 (09:20)** | **Inject 4** – Test restoration of the latest network backup fails with an unreadable snapshot error. |
| **45 (09:30)** | **Inject 5** – A social media post claims the examination is cancelled. A journalist asks whether learner information has been exposed. |
| **50–60 (09:35–09:45)** | Hot wash: evaluate against success criteria, list improvements, assign owners. |


### Measurable success criteria


| **ID** | **Criterion** | **Target** |
|---|---|---|
| **SC1** | FS01 and FIN-PC07 isolated and svc_backup disabled, with each action logged. | Within 20 minutes of declaration (by minute 20) |
| **SC2** | Every inject receives a logged decision with owner and rationale. | Within 5 minutes of the inject; 100% of injects |
| **SC3** | No service is restored or reopened from an unvalidated backup. | Zero exceptions |
| **SC4** | First written executive briefing issued; any external statement approved by LEG and EXEC before release. | Briefing by minute 30; 100% of external statements approved |
| **SC5** | Evidence-register entry (or evidence-loss note) opened for every containment action. | 100% within 10 minutes of the action |
| **SC6** | No sensitive incident detail sent over corporate email. | Zero exceptions |


## 5.2 Simulated walk-through (role by role)


*Table 14. SIMULATION: walk-through of each inject, with the view of each participant.*


| **Minute** | **Inject** | **Role-by-role walk-through (simulation)** |
|---|---|---|
| 0–10 | Declaration | **IRL:** declare Critical, open logs, start the phone tree. **SA:** EDR-isolate FIN-PC07, start sweep. **ITO:** ask for FS01 port block. **SCR:** open the incident log. **EXEC:** told by phone, asks about the exam. **COM:** ready a holding script for helpdesk. |
| 10 | 1. Management wants the portal reopened before 11:00 | **EXEC:** “Learners are waiting. Can we reopen on the last backup?” **IRL:** the last backup is unverified (E05) and the account that can reach it was used off-schedule (E03), so I advise against reopening on current storage. **BO:** I own the exam, so I need the options and the risk. **ITO:** an isolated restore from the Friday disconnected copy is possible but unproven and tight. **FOR:** a restored but infected portal destroys evidence and risks reinfection. **COM:** a late cancellation hurts more than an early one. **Outcome:** keep the 10:00 gate with five criteria. Postponement is the default. |
| 20 | 2. Attacker claims 1,800 records, 12-hour deadline | **SA:** the screenshot could be from E04’s data, from another breach, or fabricated. **FOR:** compare the screenshot’s file names and fields against FS01 and the 1.2 GB upload, once EV-06 is exported. **LEG:** do not reply or negotiate, preserve the message, and pre-assess notification (clock started at 08:45). **IRL:** treat the claim as credible but unverified, keep scope at “possible exposure”. **EXEC:** do not pay or reply without legal advice. **COM:** no public statement on data yet. **SCR:** log the time the claim was received and the deadline of 21:05. |
| 28 | 3. (My own) New mail rule, OAuth consent, and senior manager mailbox sign-in | **SA:** the attacker still has a foothold in M365, which is wider than the file server (Q1, Q5). **ITO:** revoke all sessions, remove the rule and consent, force password reset and MFA re-registration for the senior manager and finance officer. **IRL:** treat email as untrusted for all management, move updates to phone, widen the sweep to all executives. **LEG:** mailbox access is a potential personal data and privileged communication issue. **SCR:** log EV-04 export done before revocation. |
| 35 | 4. Network backup test fails (unreadable snapshot) | **ITO:** the latest network backup cannot be restored. **FOR:** possible corruption, encryption or tampering by the attacker, so preserve the snapshot as evidence. **IRL:** switch to the Friday 17:00 disconnected backup as the source (A7), and accept data loss of about 63 hours 45 minutes (A9). **BO:** I accept the loss of work since Friday for planning, but cannot confirm the exam can run. **EXEC:** informed of the revised recovery estimate. **COM:** prepare a revised learner message. |
| 45 | 5. Social post says exam cancelled. Journalist asks about exposure | **COM:** confirm the real exam position (not cancelled; under review with a decision due at the 10:00 gate and a notice by 10:15), publish that correction on the status page, and give the journalist the approved holding statement. **LEG:** wording must not say data is safe or that it was stolen. **EXEC:** approves the statement. **IRL:** log the request, no technical details. **SCR:** log the journalist’s name, time and statement given. |


## 5.3 Decision log (simulation)


*Table 15. SIMULATION: decision log with seven entries.*


| **#** | **Inject** | **Decision** | **Decision owner** | **Rationale** | **Communication** | **Effect on the response or recovery plan** |
|---|---|---|---|---|---|---|
| D1 | Start (min 0–10) | Declare Critical. Isolate FS01 and FIN-PC07 without powering off. Disable svc_backup. Cut BAK01 off the network. | IRL | Active encryption (E06), privileged account misuse (E03), and backup risk (E05). Authority is pre-delegated (A2). | Phone to CSIRT and EXEC. Log entry. | Starts SC1 clock and evidence register. Evidence-loss risk accepted and logged. |
| D2 | 1 (min 10) | Do not reopen the portal on current storage. Hold a 10:00 gate with five criteria. Default postpone. | BO (advised by IRL) | Risk of reinfection and corrupt results outweighs a delay. Delay is reversible, data corruption is not. | EXEC told verbally. Draft learner notice prepared. | Exam moves to a conditional plan. Isolated restore preparation begins in parallel. |
| D3 | 2 (min 20) | Treat the claim as credible but unverified. No reply or negotiation. Preserve the message and start phased notification preparation. | EXEC (advised by LEG) | No evidence yet of what was taken (Q3). Replying risks escalation and legal exposure. | Counsel updated. No public statement. | Q3 raised to top priority. Notification package drafted early in case it is needed by the 72-hour mark. |
| D4 | 3 (min 28) | Revoke all M365 sessions and reset credentials for finance and senior managers. Treat corporate email as untrusted for management updates. | IRL | Foothold in the identity layer could undo the containment of the file server. | Phone calls to managers. No email. | Adds identity eradication tasks and widens the sweep (Q5). Slows return to normal email. |
| D5 | 4 (min 35) | Abandon the network backup as primary source. Use the Friday 17:00 disconnected copy after validation. Preserve the failed snapshot as evidence. | IRL (BO accepts data loss) | A failed restore means the network backup cannot be trusted (E03, E05). The disconnected copy predates the earliest known event (A7). | EXEC and BO informed. Learner message updated with new exam time expected. | Recovery source and RPO change. Exam re-run moves to Day 1. |
| D6 | 5 (min 45) | Publish a correction (exam not cancelled; status to be confirmed by 10:15). Give the journalist a holding statement only. | EXEC (drafted by COM, checked by LEG) | Rumour may drive learners to the portal. A statement on data would be speculative. | Status page, SMS and journalist reply. | Starts a media log. Reinforces a single-spokesperson rule. |
| D7 | All (min 40) | Engage external DFIR and counsel at minute 40, brought forward from the planned 09:30 step in the playbook. | EXEC | Foothold in M365, an attacker claim and a failed backup together exceed the internal team’s capacity. | Provider call. EXEC informed. | Forensic collection moves to the provider. Internal team focuses on containment and recovery. |


## 5.4 Evaluation against the success criteria (simulated results)


*Table 16. SIMULATION: evaluation. These results come from my walk-through and are my own judgement.*


| **ID** | **Target** | **Simulated result** | **Assessment** |
|---|---|---|---|
| SC1 | Containment within 20 minutes | FS01 and FIN-PC07 isolated by minute 15. svc_backup disabled and BAK01 cut off by minute 19, because finding where the account was used took time. | Met (narrowly) |
| SC2 | Decision within 5 minutes of each inject | Injects 1, 3, 4 and 5 were decided within 5 minutes. Inject 2 took about 8 minutes, because counsel’s mobile number was not on the first contact sheet. | Partly met |
| SC3 | No unvalidated restore | No service was reopened. The failed backup was caught before any production use. | Met |
| SC4 | Briefing by minute 30; statements approved | The first written briefing went out at about minute 40, delayed by the minute-10 argument about reopening. External statements were all approved before release. | Partly met (briefing late) |
| SC5 | Register entry within 10 minutes | Entries for isolation and log exports were on time. The evidence-loss note for the uncaptured FS01 memory was written at about minute 50. | Partly met |
| SC6 | No sensitive detail by email | No sensitive detail was emailed. One near miss: the Scribe was about to email the decision log to the Executive Sponsor and was stopped. | Met (one near miss) |


## 5.5 Improvement plan


*Table 17. Improvements from the exercise. Target times are counted from the exercise date.*


| **#** | **Improvement** | **Priority** | **Owner** | **Target completion** | **Measurable evidence of completion** |
|---|---|---|---|---|---|
| 1 | Pre-draft the executive briefing template and the learner postponement notice, with pre-approved wording. | High | COM | 7 days | Templates approved by EXEC and LEG. In the next drill the first briefing is issued within 15 minutes. |
| 2 | Start validation of the Friday disconnected backup at declaration, in parallel with testing the network backup, not after it fails. | High | ITO | 7 days | Playbook v1.1 issued. In the next drill, validation starts by minute 15. |
| 3 | Put counsel, DFIR, provider and learner-contact sources on a printed contact card held off FS01. | High | SCR | 7 days | Cards distributed to 5 holders. A call test of all numbers passes. |
| 4 | Add an evidence-loss note template and a rule to open it within 10 minutes of any skipped capture. | Medium | FOR (with SA) | 14 days | Template in the playbook. Next drill: 100% of skipped captures have a note within 10 minutes. |
| 5 | Write a protocol for attacker claims: verification against evidence, no engagement, preservation and counsel approval. | Medium | LEG | 30 days | Protocol approved by EXEC. Next drill: decision logged within 5 minutes. |
| 6 | Add an examination continuity option (alternative venue or paper-based delivery) to the BCP, with a decision time that gives learners at least 60 minutes’ notice. | Medium | BO | 60 days | BCP section approved. A rehearsal shows an alternative sitting can be organised within one day. |
| 7 | Add EDR to all servers and create alerts for off-schedule privileged logons, new mail rules and OAuth consents. | High | SA | 30 days | Coverage report shows 100% of servers. Test alerts fire within 10 minutes. |


**Post-incident review deadline and closure.** For a real incident of this type, the structured blame-free review is held **within 14 days of incident closure** (ICDFA, n.d., slide 12), with a short “hot wash” within 72 hours of service return while memory is fresh. For this exercise the review meeting is held **5 working days** after the exercise. The Scribe keeps the action tracker. Owners submit the evidence in the last column of Table 17. The **IRL verifies** each item. The **Executive Sponsor closes** the action, consistent with the RACI (Table 8, closure and review, where EXEC is accountable). Open actions are reported at the monthly security meeting until all are closed, and the plan is re-issued with the changes (ICDFA, n.d., slide 13).

---

[⬅ Back to README](../README.md) | [⬅ Previous: Task 4 – Communication and escalation (10 marks)](04-task4-communication-and-escalation.md) | [Next: Task 6 – Case study analysis and critical reflection (10 marks) ➡](06-task6-case-study-analysis.md)
