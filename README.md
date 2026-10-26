# Phishing-Email-Analysis

## Project Overview

This project demonstrates a simulated phishing email investigation from the perspective of a junior Security Operations Center (SOC) Analyst.

The objective is to identify suspicious email characteristics, examine potential indicators of compromise (IOCs), assess the risk to an organization, and recommend appropriate incident response actions.

The investigation uses a fictional Microsoft 365 account security notification to demonstrate a common phishing scenario involving urgency, threats of account suspension, and requests for account verification.

## Objectives

- Identify common phishing indicators in email content.
- Examine sender addresses, reply-to fields, and email headers.
- Understand SPF, DKIM, and DMARC email authentication.
- Identify and document relevant indicators of compromise.
- Assess the potential impact of a phishing attempt.
- Recommend mitigation and incident response actions.
- Produce a structured incident investigation report.

## Scenario

An employee receives an email claiming that their Microsoft 365 account may be suspended unless they verify their account details within 24 hours.

The message creates urgency and threatens loss of access to encourage the recipient to act without independently verifying the request.

As the assigned junior SOC Analyst, I must investigate the message, document suspicious characteristics, determine whether the evidence supports a phishing classification, and recommend appropriate security controls.

**Safety note:** This is a simulated training scenario. The sample uses a reserved invalid domain and does not contain a live phishing destination.

## Investigation Workflow

1. **Email inspection** — Review the sender, reply-to address, subject line, greeting, wording, and requested action.
2. **Header analysis** — Examine available email routing information and authentication results.
3. **Indicator analysis** — Record relevant domains, URLs, IP addresses, and attachment hashes when present.
4. **Threat assessment** — Evaluate suspicious characteristics and potential business impact.
5. **Incident response** — Recommend containment, investigation, and remediation steps.
6. **Documentation** — Record evidence, findings, limitations, and lessons learned.

## Tools and Technologies

- **Microsoft Defender for Office 365** — Reference for email threat investigation and protection capabilities.
- **VirusTotal** — Potential analysis of appropriate, non-sensitive URLs, domains, or file hashes.
- **MXToolbox** — Reference and lookup tools for email authentication and DNS records.
- **GitHub Markdown** — Documentation of investigation evidence and findings.

Tools will be used where appropriate to the available evidence and access permissions. No live phishing emails will be sent, and no malware will be executed.

## Repository Structure

```text
Phishing-Email-Analysis/
├── README.md
├── sample-email/
│   └── simulated-phishing-email.md
├── analysis/
│   ├── email-analysis.md
│   └── indicators-of-compromise.md
├── screenshots/
└── incident-report.md
```

## Expected Deliverables

- Simulated phishing email sample.
- Email content and header analysis.
- Indicator of compromise (IOC) register.
- Risk assessment and recommended response.
- Final incident investigation report.

## Learning Outcomes

Through this project, I aim to strengthen my understanding of email-based threats, phishing detection, evidence-based investigation, threat documentation, and incident response.

This project forms part of my practical cybersecurity learning portfolio as I work toward a career in Security Operations Center (SOC) analysis.

## Ethical Considerations

This project is intended for defensive cybersecurity education. All examples are simulated, and analysis will be performed only on authorized or appropriately sanitized data.

No real credentials will be collected, no unauthorized systems will be targeted, and no malicious attachments will be executed.

## Project Status

**In progress** — The investigation will be updated as analysis, evidence collection, and documentation are completed.
