# Phishing-Email-Analysis

## Project Overview
This project demonstrates an end-to-end investigation of a high-fidelity phishing campaign targeting an enterprise environment. Acting as a junior Security Operations Center (SOC) Analyst, I triaged the email headers, dissected the social engineering mechanisms within the message body, extracted structured Indicators of Compromise (IOCs), and established SIEM hunting strategies to mitigate organizational risk.

The scenario evaluates a malicious credential-harvesting attempt spoofing a Microsoft 365 administrative security alert.

## Objectives
*   **Header Analysis:** Inspect raw email envelope metadata and analyze authentication protocol results (SPF, DKIM, DMARC).
*   **De-obfuscation & URL Triage:** Decode look-alike root domains (typosquatting) and analyze the structure of a credential-harvesting trap.
*   **Threat Intel Extraction:** Extract, document, and defang operational Indicators of Compromise (IOCs).
*   **Threat Hunting:** Author Kusto Query Language (KQL) detection queries for deployment across enterprise SIEM platforms.
*   **Incident Response:** Outline localized remediation and defensive recommendations for enterprise mail flow.

## Scenario
An enterprise user received an urgent administrative alert claiming that their organizational Microsoft 365 account password would expire within 24 hours, threatening total mailbox lockout. As the handling SOC Analyst, I retrieved the raw email data to conduct full-spectrum technical triage, confirm malicious intent, and mitigate the threat vector across the corporate directory.

## Repository Structure
```text
Phishing-Email-Analysis/
├── README.md                  (Project Overview & Lab Workflow)
├── sample-email               (Raw Evidence / Threat Actor Mail Flow)
├── email-header-analysis.md   (MTA Triage, SPF/DKIM/DMARC Routing Checks)
├── email-analysis.md          (Social Engineering & Hyperlink Deception Dissection)
└── Indicators-of-compromise.md (Defanged IOC Registry & SIEM KQL Queries)
```

## Lessons Learned 

Every phishing incident provides critical telemetry that defensive teams must use to harden the corporate attack surface.

*   **Defense-in-Depth for Email:** Mail filters cannot rely entirely on content filtering. Security protocols like **DMARC with a strict reject (`p=reject`) policy** must be enforced globally to stop look-alike domains from hitting user inboxes.
*   **The Danger of Typosquatting:** Attackers frequently place legitimate subdomains (e.g., `://microsoftonline.com`) at the front of their malicious domains to bypass casual human scrutiny. User awareness training must emphasize checking the *root domain* immediately before the first forward slash.
*   **Proactive Threat Hunting via SIEM:** Incident response shouldn't stop at the single reported email. Writing and deploying proactive **SIEM hunting queries (KQL)** ensures that silent victims who clicked the link but didn't report it are quickly identified and remediated.
*   **Automated IR Playbooks:** Reducing the Mean Time to Resolution (MTTR) requires automating the initial triage steps—such as auto-defanging links and performing automated WHOIS/reputation lookups on newly registered domains.

## Tools and Technologies
*   **Secure Email Gateway (SEG) Emulation:** Log analysis tracking envelope properties.
*   **CyberChef / WHOIS Triage:** Infrastructure lifespan profiling and domain analysis.
*   **Kusto Query Language (KQL):** SIEM queries built for enterprise-wide threat hunting.
*   **ChatGPT (AI Engineering Assistant):** Utilized to securely generate the raw synthetic email headers and mock brand-spoofing payloads to simulate true-to-life mail flow anomalies safely.
*   **GitHub Markdown:** Technical incident reporting layout.


## Lab Workflow
1.  **Evidence Collection (`sample-email`):** Staging the raw malicious email sample containing envelope routing headers and HTML payloads.
2.  **Authentication Inspection (`email-header-analysis.md`):** Tracking mail transfer agent (MTA) paths and cross-referencing SPF/DKIM validation failures.
3.  **Content Analysis (`email-analysis.md`):** Unmasking psychological social engineering hooks and breaking down subdomain link deceptions.
4.  **Threat Intel Registration (`Indicators-of-compromise.md`):** Compiling a structured, safely defanged IOC list paired with KQL detection logic.

## Project Status
**Completed** — Full-spectrum threat analysis and documentation finalized.
