# Task 4 – Communication and escalation (10 marks)


**Stage:** Preparation (communication plans) and Containment, Eradication and Recovery (executing them). Communications follow the slide guidance on internal notification, external protocols and pre-approved statements (ICDFA, n.d., slide 8), and the rule that email may be untrusted (E08). All numbers and web addresses below are **fictional**.


## 4.1 Communication matrix


*Table 13. Communication matrix. Primary channel is used while it is trusted. The alternative channel is used if corporate email is unsafe or unavailable.*


| **Stakeholder** | **Trigger** | **Message owner** | **Primary / alternative channel** | **Approver** | **Update frequency** |
|---|---|---|---|---|---|
| Learners (all 1,800; the 100 sitting the exam first) | Declaration of Critical incident, and any change to examination status. | COM | Primary: SMS broadcast and public status page. Alternative: phone call to examination cohort, notice at the campus entrance, and social media page managed by COM. | EXEC (BO for exam content) | First notice by 10:15, then every 4 hours or on any change. |
| Executive management | Declaration. Any decision requiring approval. Any change in severity. | IRL | Primary: phone call and a short written note by SMS. Alternative: in-person briefing. | IRL | Every 2 hours during Critical, or on trigger. |
| IT and security staff | Declaration. New containment instructions. | IRL | Primary: phone bridge. Alternative: group messaging on personal phones (no sensitive details). | IRL | Hourly during first 12 hours. |
| All staff | Declaration, plus when systems are isolated or loss of service is expected. | COM | Primary: SMS or phone tree. Alternative: all-hands in person, notice board, alternative mailbox. | EXEC | Twice a day, or on change. Instruction: do not use FS01, do not open unexpected attachments. |
| Service providers: external DFIR, Microsoft 365 support, backup and ISP | Containment is not confirmed within 60 minutes, or need for specialist support or provider-side logs. | ITO (DFIR: IRL) | Primary: provider emergency phone line. Alternative: named account manager on mobile. | EXEC (spend), IRL (scope) | On engagement, then at least every 4 hours. |
| Legal and privacy advisers | Suspected personal data exposure (Q3), attacker claim, regulator or media contact. | IRL | Primary: phone call. Alternative: encrypted messaging from a personal device, no email until the tenant is cleared. | IRL | On trigger, at least every 4 hours. |
| Regulator (Nigeria Data Protection Commission, if counsel advises) | Counsel assesses a notifiable breach (4.3). | LEG | Primary: the regulator’s official breach notification route. Alternative: as counsel advises. | EXEC, on LEG advice | Initial notice, then phased updates. |
| Law enforcement and national CERT | Counsel and EXEC decide to report, especially for extortion. | LEG | Primary: official reporting channel. Alternative: in-person. | EXEC | On decision, then as requested. |
| Media and public | Journalist enquiry or public post about the incident. | COM | Primary: holding statement by phone or website. Alternative: spokesperson only. | EXEC with LEG | Single statement, then updates only with approval. |


### Escalation rules


1. **E-1 Declare Critical** for ransomware, suspected exfiltration of personal data, or doubt about backup integrity. Executive Sponsor informed within 15 minutes.
2. **E-2 Legal and privacy** are consulted within 30 minutes of any suspicion that personal data may be involved.
3. **E-3 External DFIR** is engaged if containment is not confirmed within 60 minutes, or if the team cannot scope the incident, or if Critical lasts 4 hours.
4. **E-4 Examination decision gate** at 10:00 and any later gate the Business Owner sets. If criteria are not met, the examination is postponed.
5. **E-5 Media, regulator, law-enforcement and attacker contact** is handled only by COM, LEG and EXEC. Staff pass all enquiries to COM. No one replies to the attacker without LEG and EXEC approval.
6. **E-6 If email is suspected**, no sensitive detail is sent by email. Switch to the alternative channel on the matrix.
7. **E-7 Severity change** (up or down) is announced to the matrix groups listed for that level, and logged with the reason.

## 4.2 Executive briefing and learner notice


*Executive briefing draft (158 words; required 150–200). Prepared for 09:30 in the plan, on the assumption that the steps in playbook rows 3–7 are under way.*


> Executive briefing – 09:30 WAT, Monday (Day 0). Classification: Critical (provisional).
>
> **Confirmed:** Ransomware-type encryption has affected the finance workstation FIN-PC07 and the shared file server FS01, and a ransom note is present (E06). The learning portal loads, but learners cannot open materials or submit work (E07). Our incident contact list was on FS01 and is unavailable (E08). The 11:00 examination for 100 learners is at risk.
>
> **Uncertain:** We do not yet know how the attacker entered, whether learner or finance data left our network (a 1.2 GB upload occurred, E04), whether the backup system was tampered with (E03), or whether email can be trusted.
>
> **Actions under way:** Affected systems are isolated, the backup account is disabled, and evidence is being preserved.
>
> **Decisions needed by 10:00:** (1) approve postponing the 11:00 examination unless the portal is verified safe; (2) approve engaging an external forensic provider; (3) authorise legal counsel to assess notification duties.
>
> **Next update:** 10:30 WAT, by phone.


*Learner notice draft (123 words; required 100–150). Written for the “postpone” outcome at the 10:00 gate. If the gate is passed, only the examination paragraph changes.*


> Notice to learners – Monday, 10:15 WAT
>
> Northbridge Skills Institute is dealing with a technical security incident affecting some of our systems.
>
> **Your examination:** the 11:00 online examination will **not** take place at that time. Your place is protected and a new date will be confirmed by 14:00 today.
>
> **What to do:** Please do not log in to the learning portal today. Ignore any message, text or social media post about the examination, results or payments unless it comes from the sources below. Never click links or share passwords.
>
> **Official updates:** www.northbridge.example/status or the helpdesk on +234 000 000 0000 (fictional), 08:00–18:00.
>
> We have no confirmed evidence yet that your personal information has been accessed. We will tell you promptly if that changes.


## 4.3 Notification obligations: how legal and privacy advisers will decide


**Operational notices versus formal breach notification.** The notices above (learners, staff, executives and providers) are **operational**. They tell people what to do and what service to expect, and they say what is and is not known. A **formal breach notification** is a legal act to a regulator and, if required, to data subjects. It has its own content, deadline and approval, and it is decided by counsel and the Executive Sponsor (RACI: LEG responsible, EXEC accountable). The operational learner notice does not state that data has been stolen, because that is unconfirmed (Q3), and it does not state that data is safe, because that is also unconfirmed.


**Process.**


1. **Facts.** I give counsel a short fact sheet every 4 hours: what data sets sit on FS01, FIN-PC07 and M365, what is confirmed, what is not, and the status of Q3 (what was in the upload).
2. **Applicability and jurisdiction.** Counsel confirms who the data controller and processors are, the law that applies and any contractual duties, including those to learners in other countries and to sponsors or accreditors (**unresolved**; assumption A1 is Nigeria).
3. **Risk assessment.** Counsel decides whether the breach is likely to risk the rights and freedoms of learners, and whether the risk is high, using the data types, volume, the extortion claim and whether data was encrypted or already exposed.
4. **Recipients and deadlines.** Counsel confirms recipients (regulator, data subjects, any partners) and the deadline, and the Scribe records the “time of awareness” and the reasoning.
5. **Content and approval.** LEG drafts, EXEC approves, COM issues. The notification can be phased as facts emerge.

**Jurisdiction and source (assumption A1).** If Northbridge is a Nigerian data controller, then, as summarised by a secondary legal commentary on the Nigeria Data Protection Act 2023 (NDPA), section 40(2) requires the controller to notify the Nigeria Data Protection Commission **within 72 hours** of becoming aware of a breach that is likely to risk the rights and freedoms of data subjects, with information provided in phases if needed, and section 40(3) requires data subjects to be told **immediately** where the risk is high (Federal Republic of Nigeria, 2023; Afriwise, n.d.). As a precaution, I start a record of the 72-hour clock at the 09:30 briefing, from 08:45 on Day 0, so the working outer limit would be 08:45 on Thursday (Day 3); counsel determines the true time of awareness. These section references come from a secondary summary, so counsel must check them against the official Act text and any Commission guidance before they are relied on. I do not assert a deadline for any other jurisdiction.

---

[⬅ Back to README](../README.md) | [⬅ Previous: Task 3 – Response playbook and evidence preservation (25 marks)](03-task3-playbook-and-evidence.md) | [Next: Task 5 – Tabletop exercise and improvement plan (15 marks) ➡](05-task5-tabletop-exercise.md)
