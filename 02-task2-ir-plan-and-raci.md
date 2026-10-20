# Task 2 – Incident response plan and team responsibilities (20 marks)


**Stage:** Preparation. The plan follows the core components on slide 14 (mission and structure; roles and escalation; communication protocols; resource requirements) (ICDFA, n.d., slide 14). NIST SP 800-61 Revision 3 frames incident response as part of wider cyber risk management, where Govern, Identify and Protect support preparation and Detect, Respond and Recover make up incident response (NIST, 2025). Table 5 maps the two views so the reader can see where each part of my plan sits.


*Table 5. Mapping of the teaching stages to CSF 2.0 functions as used in NIST (2025). The mapping is my own reading, not a NIST statement.*


| **Teaching stage (ICDFA, n.d., slide 6)** | **CSF 2.0 function (NIST, 2025)** | **Where it appears in this report** |
|---|---|---|
| 1. Preparation | Govern, Identify, Protect (supporting) | Task 2 policy, CSIRT, RACI, readiness checklist |
| 2. Detection and analysis | Detect, with Identify for asset knowledge | Task 1; Task 3 investigation steps |
| 3. Containment, eradication and recovery | Respond and Recover | Task 3 playbook and acceptance criteria; Task 4 communications |
| 4. Post-incident activity | Improvement feeds all functions | Task 5 improvement plan and review; Task 6 |


## 2.1 Incident response policy and plan outline


*Table 6. Policy and plan outline for Northbridge Skills Institute.*


| **Element** | **Policy and plan content** |
|---|---|
| **Mission** | Protect learners, learner data and the institute’s ability to teach and assess by detecting, containing and recovering from security incidents quickly, lawfully and with evidence that stands up to scrutiny. |
| **Objectives** | (1) Declare and classify within 15 minutes of credible report. (2) Contain active spread within 30 minutes. (3) Preserve evidence for every containment step. (4) Keep stakeholders informed on a published cycle. (5) Restore only validated systems, approved by the business owner. (6) Complete a blame-free review within 14 days of closure (ICDFA, n.d., slide 12). |
| **Scope** | All Northbridge information assets: FIN-PC07 and other endpoints, FS01, LMS01, BAK01, Microsoft 365 identity and email, third-party services and personal data of learners and staff. Applies to staff, contractors and providers with access. |
| **Incident declaration** | Any staff member may report. The Incident Response Lead (IRL) declares an incident when there is credible evidence of compromise of confidentiality, integrity or availability (ICDFA, n.d., slide 4). Severity (Table 2) is assigned at declaration and reviewed at least every 2 hours. |
| **Activation and escalation** | Critical: IRL activates the full CSIRT by phone tree and informs the Executive Sponsor within 15 minutes. High: core CSIRT and management informed. Medium and Low: ticketed. Automatic Critical triggers: ransomware, privileged-account misuse with data staging, doubt about backup integrity, or suspected personal data exposure. Escalate to external DFIR if containment is not confirmed within 60 minutes. |
| **Authority to isolate** | The IRL (deputy: IT Operations Lead) may isolate any endpoint, server, account or network segment without prior approval where there is active harm (A2). The Executive Sponsor is informed within 15 minutes. Decisions are logged with time, reason and expected business impact. Restoring service requires business owner approval, not IRL approval alone. |
| **Documentation** | A single incident log (time, actor, action, reason) kept by the Scribe, on paper or an offline device until corporate tools are trusted. Evidence register and chain-of-custody forms. Decision log. Notification record with timestamps. Impact assessment (operational, financial, reputational) (ICDFA, n.d., slide 13). |
| **Review** | Plan reviewed annually and after every Critical or High incident, and after every tabletop. Contact list verified monthly. Backup restoration tested quarterly. Version control and sign-off by the Executive Sponsor. |


**Connection to business continuity.** This plan and the business continuity plan (BCP) share the same trigger and decision gate. A Critical incident also invokes the continuity decision on the examination (Task 3, Decision 2). The BCP supplies the business impact analysis inputs that the IR plan uses for recovery order and targets: recovery time objectives (RTO), recovery point objectives (RPO) and manual workarounds (for example a rescheduled or paper-based examination) (ICDFA, n.d., slide 18). IR decides what is safe, and BCP decides how the institute operates in the meantime. The business owner approves service return.


## 2.2 CSIRT structure


*Table 7. CSIRT roles. Role holders are fictional placeholders. Core members are on-call for Critical incidents.*


| **Role (abbreviation)** | **Held by (fictional)** | **Main responsibilities** |
|---|---|---|
| Incident Response Lead / Incident Commander (IRL) | Francisca Umejesi (this plan’s author) | Declares and classifies, leads operations, holds isolation authority, makes critical decisions, briefs executives (ICDFA, n.d., slide 15). |
| Security Analyst (SA) | Institute security analyst (1 post) | Triage, log analysis, EDR hunting, indicator sweeps, containment actions. |
| Forensics Lead (FOR) | External DFIR provider (A3), with the SA as first-responder until arrival | Evidence acquisition, integrity and custody, malware analysis, supports legal proceedings. |
| IT Operations Lead (ITO) | Senior IT staff member (1 of 3) | Network isolation, account resets, rebuilds, restores, backup validation. |
| Business Owner / Academic Registrar (BO) | Head of Examinations | Owns the examination and service priorities, approves restoration and return to service. |
| Legal and Privacy Adviser (LEG) | External counsel and the institute’s data protection officer | Notification obligations, privilege, regulator and law enforcement liaison, ransom-payment legal advice. |
| Communications Lead (COM) | Marketing and Communications Manager | Stakeholder notices, media holding statements, social media monitoring (ICDFA, n.d., slide 15). |
| Executive Sponsor (EXEC) | Director of the Institute | Accountable for risk acceptance, regulatory decisions, budget and external engagements. |
| Scribe and Evidence Custodian (SCR) | Administrative officer, trained | Keeps the incident log, decision log and evidence register. Holds the evidence store key. |


**Getting extra support with a small team.** Northbridge has three IT staff and one security analyst, so surge capacity must come from outside. (1) An external DFIR retainer or emergency call-out agreement, assumed reachable in about two hours (A3), recommended as a readiness action. (2) The Microsoft 365 provider’s support channel for tenant-level investigation. (3) The backup, network and ISP providers named on the printed contact card. (4) The national CERT and law enforcement, as advised by legal counsel. (5) Business staff trained as runners and note-takers so technical staff stay on technical work. Escalation to external help is automatic if containment is not confirmed within 60 minutes or if Critical severity persists for 4 hours.


## 2.3 RACI matrix


R = Responsible (does the work), A = Accountable (single owner who answers for the outcome and approves), C = Consulted (two-way input before action), I = Informed (told after) (ICDFA, n.d., slide 15). A/R means one role is both. Each row has **exactly one A** and at least one R.


*Table 8. RACI matrix for ten activities. A dash means not involved.*


| **Activity** | **IRL** | **SA** | **FOR** | **ITO** | **BO** | **LEG** | **COM** | **EXEC** | **SCR** |
|---|---|---|---|---|---|---|---|---|---|
| **Detection and triage** | A | R | I | R | – | – | – | I | – |
| **Analysis and scoping** | A | R | R | C | C | C | I | I | I |
| **Containment and isolation** | A/R | R | C | R | C | I | I | I | I |
| **Evidence handling and custody** | A | R | R | R | – | C | – | – | R |
| **Stakeholder communication** | A | I | – | I | C | C | R | C | I |
| **Assessment of reporting obligations** | C | – | C | – | I | R | I | A | I |
| **Eradication and credential reset** | A | R | C | R | I | – | I | I | I |
| **Restoration approval** | R | C | C | R | A | I | I | C | I |
| **Exam continuity decision** | R | I | – | C | A | C | C | C | I |
| **Closure and post-incident review** | R | C | C | C | C | C | C | A | R |


*Key: IRL Incident Response Lead; SA Security Analyst; FOR Forensics Lead; ITO IT Operations Lead; BO Business Owner; LEG Legal and Privacy Adviser; COM Communications Lead; EXEC Executive Sponsor; SCR Scribe and Evidence Custodian. Red cells show the single Accountable role. Green cells show Responsible roles.*


**Design choices.** The IRL is accountable for operational activities, as on slide 15, but not for regulatory decisions (EXEC, because the institute is the controller) or service return (BO, because the business bears the risk). Restoration approval has IRL and ITO responsible for recommending and executing, and the BO accountable for deciding. This stops the technical team from approving its own work.


## 2.4 Readiness checklist and preparation improvements


*Table 9. Preparation improvements. The resources column lists what is needed, without invented prices. Owners are roles.*


| **#** | **Improvement** | **Owner** | **Resources needed** | **How readiness is checked** |
|---|---|---|---|---|
| 1 | **Backup readiness.** Keep at least one offline or immutable copy of FS01, LMS01 and M365 data. Remove standing admin reach from svc_backup. Define RTO and RPO per system from the BIA. | ITO (accountable: EXEC) | Immutable or offline storage, backup software settings, time to design and approve RTO and RPO. | Documented restoration test of a full system every quarter, timed against RTO. Evidence report filed. No test older than 90 days. |
| 2 | **Accessible incident contact list.** Hold a printed and an offline copy, not only on FS01. Include staff mobiles, providers, counsel, DFIR and regulators. | Scribe | Printed cards, sealed envelopes with IRL, ITO and Director, a personal-device encrypted copy. | Monthly call test of ten random numbers, with the result logged. Contact list kept off the production file server. |
| 3 | **Detection tools.** Extend EDR to all servers, centralise logs (including proxy, M365 and Windows security) with alerts for off-schedule privileged logons and large uploads. | SA | EDR licences for servers, log collection or lightweight SIEM, alert rules. | Coverage report shows 100% of servers and workstations. Test alert fires within 10 minutes in a controlled test. |
| 4 | **Secure communication.** Pre-agree an out-of-band channel (phone tree, SMS service, and an alternative mailbox outside the primary tenant) and a public status page that does not depend on LMS01. | COM | Alternative email domain or mailbox, SMS gateway or broadcast list, template library. | Quarterly drill: IRL sends a test notice to the CSIRT and a sample of learners within 15 minutes using only the alternative channel. |
| 5 | **Privileged access.** Vault and rotate service credentials, enforce MFA and conditional access for admins and finance staff, and remove admin rights where not needed. | ITO | Password vault, conditional access policies, access review time. | Quarterly access review. Report of all accounts with admin rights. Sign-in policy test. |
| 6 | **Training and exercise.** Role-specific CSIRT training, phishing awareness for all staff, and a tabletop at least once a year (ICDFA, n.d., slide 8). | IRL | Half-day workshops, phishing simulation tool, exercise scenario. | Attendance 100% of CSIRT. Phishing report rate trend. Tabletop actions closed on time. |
| 7 | **Forensics and legal readiness.** Contract an external DFIR provider and legal counsel with incident terms, and prepare evidence-handling kit (write blockers, encrypted storage, forms). | EXEC | Signed retainer or call-out agreement, evidence jump kit. | Provider response time confirmed in a call test. Kit inventory checked every six months. |

---

[⬅ Back to README](../README.md) | [⬅ Previous: Task 1 – Incident classification and initial assessment (15 marks)](01-task1-incident-classification.md) | [Next: Task 3 – Response playbook and evidence preservation (25 marks) ➡](03-task3-playbook-and-evidence.md)
