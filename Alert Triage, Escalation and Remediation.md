# Junior Security Analyst Intro — Alert Triage

**Date completed:** 9th August 2026
**Platform:** TryHackMe — SOC Level 1 path, Junior Security Analyst Intro module
**Category:** SOC alert triage / incident escalation

## Objective
Investigate a security alert, identify a malicious IP address, escalate 
it through the correct process, and take remediation action by blocking 
it at the firewall.

## Approach
1. **Alert review** — Opened the alert dashboard and reviewed the flagged 
   activity to identify indicators of compromise.
2. **IP identification** — Cross-referenced the alert details to isolate 
   the malicious source IP.
3. **Escalation** — Escalated the finding to the appropriate contact per 
   the incident response workflow, rather than acting unilaterally.
4. **Remediation** — Blocked the malicious IP at the firewall and 
   confirmed the block was successful.

## Key takeaway
This task reinforced the standard SOC workflow: **detect → escalate → 
remediate**. Escalation matters because a Tier 1 analyst typically 
doesn't act alone, confirming with a senior analyst or following the 
runbook is part of the job, not a formality.

## Screenshot <img width="1882" height="1587" alt="Screenshot 2026-08-09 122420" src="https://github.com/user-attachments/assets/64fc763c-1963-4969-8b48-9a3bd3356d16" />


*Alert dashboard showing the identified malicious IP prior to escalation.
