# Task 6 – Case study analysis and critical reflection (10 marks)


*Analysis of the healthcare ransomware case, slide 16 (325 words; required 300–400).*


The slide 16 case describes a 2,500-employee healthcare organisation hit by a Ryuk-variant ransomware after a phishing email (ICDFA, n.d., slide 16). Three strengths stand out. First, offline backups let it recover without paying. Second, segmentation limited spread, and EDR alerts triggered immediate IR team activation. Third, a prepared team, playbooks and timely regulatory notifications supported disciplined response.


There are two limitations. Malware moved laterally for 72 hours before detection (Day 1 to Day 4), so detection was weak and the attacker had a long window to steal data. Total downtime still reached seven days. Also, “no patient data exfiltration confirmed” is not evidence of absence: the slide gives no evidence base, and it does not say when the 72-hour and seven-day clocks start.


I would transfer two changes to Northbridge. First, offline or immutable backups with scheduled restoration tests, because Northbridge’s backups are neither immutable nor tested within 90 days, and E03 and E05 show how uncertain they are. Second, earlier detection through EDR on all servers plus segmentation, because Northbridge’s server coverage is incomplete and FS01 encryption was noticed only when users saw files change (E06).


Restoring critical systems within 72 hours differs from seven-day full restoration. The first returns minimum essential services, which is an RTO-style target measured for priority services only. Full restoration also covers lower-priority systems, rebuilds, integrity validation and enhanced monitoring before normal operation resumes.


Before claiming no patient data was stolen, I would need evidence covering the whole dwell period: complete proxy, firewall and DNS logs showing no unexplained outbound transfers; EDR file-access telemetry; file-server audit logs; forensic review of affected hosts; and no leak-site or attacker claims. Missing or short-retention logs would block that claim, because absence of evidence is not evidence of absence.


After the tabletop, I would revise my backup decision: I would validate the Friday disconnected backup in parallel from the start, not wait for the network backup test to fail at minute 35.

---

[⬅ Back to README](../README.md) | [⬅ Previous: Task 5 – Tabletop exercise and improvement plan (15 marks)](05-task5-tabletop-exercise.md) | [Next: References ➡](07-references.md)
