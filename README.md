# Post-Engagement Debrief and Remediation Tracking Report

**Red Team Project — CY376: Network Monitoring, Security and Auditing**

## Summary

A controlled red team engagement against a deliberately vulnerable web application (DVWA), deployed in an isolated Docker container. Three vulnerability classes were tested through manual exploitation — SQL injection, OS command injection, and brute-force authentication — and each finding was carried through a full post-engagement debrief and a remediation tracking framework with assigned severity, ownership, and deadlines.

## Author

- **Name:** DAMIAN SEYRAM SOSAVI
- **Index Number:** FCM.41.018.243.23

## Tools Used

- **Docker** — container runtime for the isolated lab
- **vulnerables/web-dvwa** — the target application (Damn Vulnerable Web Application)
- **VirtualBox** — attempted Kali Linux VM for automated brute-force testing (see Limitations)
- Manual browser-based exploitation (Chrome) and the DVWA container's own Apache access logs as evidence

## Repository Structure

```
.
├── README.md
├── docs/
│   └── Post-Engagement_Debrief_and_Remediation_Tracking_Report.pdf
├── evidence/
│   ├── screenshots/        # Figures 1-17 referenced in the report
│   └── logs/
│       └── access_log_excerpt.txt
├── diagrams/
│   └── lab_architecture.png
├── presentation/
│   └── Post-Engagement_Debrief_Presentation.pptx
└── .gitignore
```

## How to Run the Lab

```bash
docker run --rm -it -p 80:80 vulnerables/web-dvwa
```

Then visit `http://localhost` in a browser, log in with the default credentials (`admin` / `password`), go to **DVWA Security**, and set the security level to **Low** before testing.

## Key Findings (see full report in `docs/`)

| ID | Finding | Severity | Owner | Due |
|----|---------|----------|-------|-----|
| RT-01 | SQL Injection — logic bypass & credential exfiltration | Critical | Dev/DB Team | 3 days |
| RT-02 | OS Command Injection (RCE) | Critical | Dev Team | 3 days |
| RT-03 | No account lockout on login | High | Security/Dev Team | 7 days |

## Evidence

Key screenshots are in `evidence/screenshots/`, referenced by figure number in the full report. Highlights:

- SQL Injection full credential dump: `evidence/screenshots/figure-11-sqli-union-hashes.png`
- Command Injection (`www-data` returned): `evidence/screenshots/figure-08-command-injection.png`
- Brute force GET-based credential exposure: `evidence/screenshots/figure-14-url-bar-wrongpass.png`

## Limitations

The original plan was to automate the brute-force test with Hydra from a Kali Linux VM. That VM failed to boot due to a VirtualBox/Docker Desktop virtualisation conflict on the host machine (see `evidence/screenshots/figure-17-kali-vm-error.png`). Testing was completed manually instead — see Section 4.3 of the full report for details.

## Scope

All testing was performed against a local, isolated Docker container under my own control. No real, unauthorised, or third-party system was tested at any point.
