# SOC Role in Blue Team — Role Assignment Exercise

**Date completed:** 9th August, 2026
**Platform:** TryHackMe — SOC Level 1 path, SOC Role in Blue Team module
**Category:** Blue Team structure / role responsibilities

## Objective
Match seven real-world security scenarios to the correct specialist role 
within a Blue Team, demonstrating understanding of how responsibilities 
are divided across a security organization — not every task belongs to 
a SOC analyst.

## Roles covered in this exercise
- **SOC Engineer** — maintains and troubleshoots security tooling (e.g. 
  SIEM availability issues)
- **CERT Lead** — leads incident response for active/urgent threats
- **GRC Auditor** — governance, risk, and compliance checks
- **Penetration Tester** — proactively tests systems for vulnerabilities
- **Threat Researcher** — analyzes threat actor groups and their tactics

## Approach
Worked through each scenario by asking: *is this reactive incident 
handling, proactive testing, compliance, or threat intelligence?* — then 
matched it to the role whose remit that falls under. For example:
- A firewall brute-force alert needing triage → incident response role
- A new system needing a vulnerability check before release → 
  Penetration Tester
- SIEM downtime from a storage limit → SOC Engineer (tooling/infrastructure 
  ownership, not analyst-level triage)
- A named threat group (FIN7) targeting the company → Threat Researcher 
  (tactics analysis, not incident handling)

## Key takeaway
A SOC isn't one job — it's several distinct specialisms that hand off to 
each other. Knowing *who* to escalate to, and why, is as important as 
knowing how to triage an alert yourself. This matters practically: a 
Tier 1 analyst who routes things to the wrong specialist slows down 
response time.

## Screenshot <img width="3160" height="1785" alt="Screenshot 2026-08-09 133710" src="https://github.com/user-attachments/assets/e77ab9b1-cae6-48e5-b0e1-b14af6f8821f" />


*All seven scenarios matched to their correct specialist role — e.g. 
CERT Lead for active ransomware response, GRC Auditor for compliance 
audits, Threat Researcher for named threat-actor analysis.*
