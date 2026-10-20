# Northbridge Skills Institute – Incident Response Plan

**GRC205 Incident Management and Business Continuity – Week 20 Incident Response Planning Assignment**
International Cybersecurity and Digital Forensics Academy (ICDFA) · Individual assignment (100 marks, 20% of course grade)

> **Fictional scenario.** Northbridge Skills Institute, all names, systems, contact details and results are fictional. All evidence collection is described as *planned*; no acquisitions were performed and no hash values are claimed. The Task 5 tabletop is a **simulation**.

## Submission details

| Item | Detail |
|---|---|
| Student name | Francisca Umejesi |
| Student ID | 2025/GCR/12816 |
| Official email | gcr2512816@students.icdfa.edu.ng |
| Role adopted | Incident Response Lead, Northbridge Skills Institute (fictional) |
| Word count | 11,384 words (body text and tables, excluding references and declaration)

## Repository contents

| # | Document |
|---|---|
| 0 | [Reading guide and assumptions](docs/00-assumptions-and-reading-guide.md) |
| 1 | [Task 1 – Incident classification and initial assessment (15 marks)](docs/01-task1-incident-classification.md) |
| 2 | [Task 2 – Incident response plan and team responsibilities (20 marks)](docs/02-task2-ir-plan-and-raci.md) |
| 3 | [Task 3 – Response playbook and evidence preservation (25 marks)](docs/03-task3-playbook-and-evidence.md) |
| 4 | [Task 4 – Communication and escalation (10 marks)](docs/04-task4-communication-and-escalation.md) |
| 5 | [Task 5 – Tabletop exercise and improvement plan (15 marks)](docs/05-task5-tabletop-exercise.md) |
| 6 | [Task 6 – Case study analysis and critical reflection (10 marks)](docs/06-task6-case-study-analysis.md) |
| 7 | [References](docs/07-references.md) |
| 8 | [Authorship and AI declaration](docs/08-authorship-and-ai-declaration.md) |

The Word file in `submission/` contains the same content as the Markdown files.

## Summary of the response

- **Incident:** suspected ransomware with suspected exfiltration (E04), suspected account and backup compromise (E02, E03, E05); rated **Critical (provisional)** at 08:45 WAT on Day 0.
- **Plan (Task 2):** policy outline, nine-role CSIRT, 10-activity RACI (one Accountable per row), seven-item readiness plan.
- **Playbook (Task 3):** 19 ordered actions, two justified decisions (isolate while preserving evidence; examination go/no-go gate at 10:00), planned evidence register EV-01 to EV-08, recovery order and acceptance criteria.
- **Communications (Task 4):** nine-group matrix with alternative channels, escalation rules, executive briefing, learner notice, notification process (Nigeria assumed; see assumption A1).
- **Tabletop (Task 5):** 60-minute simulated exercise with the four required injects plus one of my own, seven logged decisions, evaluation and seven improvements.
- **Case study (Task 6):** critique of the slide 16 healthcare ransomware case and what I would change.

## Frameworks and sources

Structured by the four teaching stages (ICDFA, n.d., slide 6). NIST SP 800-61 Revision 3 is cited only for its CSF 2.0 alignment, and the CISA #StopRansomware Guide and the Nigeria Data Protection Act 2023 support specific decisions. Full list: [references](docs/07-references.md).

## Authorship and AI declaration

See [docs/08-authorship-and-ai-declaration.md](docs/08-authorship-and-ai-declaration.md).
