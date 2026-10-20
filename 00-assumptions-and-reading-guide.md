# Reading guide and assumptions

## How to read this report


Every claim about the incident is labelled so that the reader can see what is known and what is not. **Confirmed** means directly observed in the evidence pack (E01–E08). **Hypothesis** means a reasoned working explanation that still needs testing. **Unresolved** means an open question with a named check. **Assumption** (A1–A10, below) means a fact I have supplied because the brief is silent; each is labelled where it is used. All names, contact details and times are fictional. All evidence collection is described as **planned**; nothing in this report claims that an acquisition was performed or that a hash value exists. The report is organised by the four teaching stages (preparation; detection and analysis; containment, eradication and recovery; post-incident activity) (ICDFA, n.d., slide 6). Where NIST SP 800-61 Revision 3 is cited, it is used only for its CSF 2.0 alignment, not for the four-stage model (NIST, 2025).


### Assumptions register


| **ID** | **Assumption (not in the brief)** | **Used in** |
|---|---|---|
| A1 | Northbridge is a data controller operating in Nigeria, so the Nigeria Data Protection Act 2023 is the working legal reference. Legal counsel must confirm this and check any contractual or foreign-learner duties. | Task 4 |
| A2 | The Incident Response Lead (me) holds pre-delegated authority to isolate systems without waiting for executive sign-off, with the Executive Sponsor informed within 15 minutes. | Tasks 2, 3 |
| A3 | An external digital forensics and incident response (DFIR) provider can be engaged within about two hours, whether through a retainer or an emergency call-out. No retainer exists today. | Tasks 2, 3 |
| A4 | The finance officer is a victim, not a malicious insider. This is a working position, tested by interview, and it does not imply fault. | Task 1 |
| A5 | Learner mobile numbers can be reached from a source outside FS01 (for example the M365 directory or a student-record export). This must be verified in the first hour. | Tasks 3, 4 |
| A6 | The online examination uses LMS01 for delivery and stores submissions on FS01, as the brief states that the portal depends on FS01 files. | Tasks 1, 3 |
| A7 | The Friday 17:00 disconnected backup predates the intrusion, because the earliest known event is E01 on Sunday 16:40. Dwell time before E01 is unknown, so this is validated before use. | Task 3 |
| A8 | Staff mobile phone numbers are held personally by the IT team and management, so the phone tree can start immediately (E08 confirms phones work). | Task 3 |
| A9 | The business accepts re-sitting or re-submitting work created after Friday 17:00 if the Friday disconnected backup is the only trustworthy source. | Task 3 |
| A10 | Exercise minute 0 equals 08:45 WAT on Day 0, and exercise minutes map to scenario clock time one-to-one. | Task 5 |

---

[⬅ Back to README](../README.md) | [Next: Task 1 – Incident classification and initial assessment (15 marks) ➡](01-task1-incident-classification.md)
