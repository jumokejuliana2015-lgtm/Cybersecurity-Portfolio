# Deploying & Administering a Splunk Enterprise SIEM on Kali Linux

**Date:** Feb 2026
**Environment:** Kali Linux (VirtualBox), Splunk Enterprise 10.2.0
**Category:** SIEM deployment / role-based access control / log analysis

## Objective
Independently install Splunk Enterprise, resolve a real dependency error 
during setup, design and test a role-based access control model with 
multiple accounts, and use the platform to search and analyze ingested 
log data — covering the full path from infrastructure to analyst-level 
use of the tool.

## Part 1: Installation & Troubleshooting
Downloaded the Splunk `.deb` package via `wget` and installed with 
`dpkg -i`. First launch failed with `libcrypto.so.3: version 
'OPENSSL_3.4.0' not found`. Diagnosed this as a package dependency 
conflict rather than reinstalling blindly — ran `apt --fix-broken 
install`, which resolved it. Created the administrator account 
interactively, confirmed all preliminary checks passed, and verified 
the web interface came up at `http://kali:8000`. Enabled boot-start so 
the service persists across VM restarts.

## Part 2: Role-Based Access Control

**Testing a built-in role restriction.** Created a second account 
("Simon Peter") assigned the built-in `power` role instead of `admin`, 
then logged in as that user to verify — not just assume — the 
restriction worked. Confirmed the homepage showed fewer options (12 
recommended items vs. the administrator's 16), with "Add data," 
"Manage permissions," and "Manage alerts" all absent.

**Designing a custom role from scratch.** Rather than relying only on 
Splunk's built-in roles, used the role builder to review the full 
capability list (dozens of individually toggleable permissions such as 
`edit_tcp`, `list_all_users`, `install_apps`) and understand how a 
role's access is actually composed — access control here isn't a 
single switch, it's a granular set of capabilities.

**Provisioning against the custom role.** Created a third account 
("Judas Iscariot") and assigned a custom role, `soc_tier_1_analyst`, 
built specifically for this exercise — modeling how a SOC would 
provision a junior analyst with only the capabilities that role 
actually needs, rather than defaulting to `power` or `admin`.

**Verifying at scale.** Provisioned two further accounts (John Mark, 
James Zebedee) and logged in as each to confirm consistent, predictable 
behavior across multiple provisioned users — not just a one-off test.

**Reviewing the full access model.** Pulled up the Users admin table 
showing all five accounts side by side — roles, authentication type, 
last login, and status — the kind of view an admin would audit 
periodically to catch stale or over-privileged accounts.

## Part 3: Securing the Web Interface
Generated a self-signed certificate and private key with OpenSSL 
(`openssl req -newkey rsa:2048 ...`) as a first step toward serving 
Splunk's web UI over TLS rather than leaving it on plain HTTP.

## Part 4: Log Search & Analysis
Ran a search against an ingested OpenSSH log source 
(`source="OpenSSH3000.csv" host="kali" index="openssh"`), returning 
3,000 events. Reviewed the event stream for patterns — failed logins 
against invalid users, authentication failures across multiple hosts 
(auth-gateway, db-server, bastion-host, web-server, api-node), and 
disconnects — the kind of raw material a SOC analyst triages daily.

## Key takeaway
Standing up Splunk is the easy part. The more relevant skills here are 
designing least-privilege access (building a role around what a job 
actually needs, not reusing `power` for convenience), verifying that 
access controls behave as intended rather than trusting the 
configuration screen, and using the platform to actually search and 
reason about log data — the same habits that matter in a live SOC.

## Screenshots
 <img width="1520" height="591" alt="Screenshot 2026-02-13 141630" src="https://github.com/user-attachments/assets/7078de8f-7062-4903-a601-ad93cfe301f1" />

*Dependency error on first launch — resolved via `apt --fix-broken install`.*

 <img width="2450" height="1343" alt="Screenshot 2026-02-13 142045" src="https://github.com/user-attachments/assets/53bb3de5-8fc0-45c5-bddf-0b3d044cb469" />

*Administrator account created, preliminary checks passed, web interface confirmed live.*

 <img width="1867" height="1858" alt="Screenshot 2026-02-13 231631" src="https://github.com/user-attachments/assets/3bebaa0a-f584-4998-9465-e30d9590de9e" />

*Reviewing Splunk's granular capability list while building a custom role.*

 <img width="1888" height="1893" alt="Screenshot 2026-02-15 194607" src="https://github.com/user-attachments/assets/74a5a0a7-1248-4b29-b4b2-1e0f8c23e2b1" />

*New account assigned the custom `soc_tier_1_analyst` role rather than a built-in default.*

 <img width="1996" height="1918" alt="Screenshot 2026-02-13 232253" src="https://github.com/user-attachments/assets/07806978-2204-43c7-9894-b5f7f84d6836" />

*Logged in as the power-role user — no Add data, Manage permissions, or Manage alerts.*

 <img width="2040" height="1914" alt="Screenshot 2026-02-13 232235" src="https://github.com/user-attachments/assets/37e68cf9-477b-4b7f-8b01-0264efc05034" />

*Same homepage as Administrator, showing the full option set for comparison.*

 <img width="1888" height="1893" alt="Screenshot 2026-02-15 194607" src="https://github.com/user-attachments/assets/b55eba07-f50d-4fca-9702-6f949772a8f1" />

*All five provisioned accounts with roles, auth type, and last login — an access audit view.*

 <img width="1886" height="1862" alt="Screenshot 2026-02-17 073817" src="https://github.com/user-attachments/assets/b469f307-8791-4561-9bce-d9025bc960ed" />

*Generating a self-signed cert and key as a first step toward TLS.*
 
  <img width="1807" height="1645" alt="Screenshot 2026-02-16 070300" src="https://github.com/user-attachments/assets/a735a0fa-36aa-4413-9234-d9993ad6e423" />

*Searching 3,000 ingested OpenSSH events for failed logins and disconnects.*
