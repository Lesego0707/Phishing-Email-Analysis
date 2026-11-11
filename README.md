 Phishing-Email-Analysis

## Project Overview

This project demonstrates a simulated phishing email investigation conducted from the perspective of a Junior Security Operations Center (SOC) Analyst.

The investigation focuses on a credential-harvesting attempt impersonating a Microsoft 365 administrative security alert. The exercise involves examining raw email headers, analysing social engineering techniques, identifying suspicious URLs, extracting Indicators of Compromise (IOCs), and developing Kusto Query Language (KQL) detection queries for SIEM-based threat hunting.

The project demonstrates a structured approach to phishing email triage, threat identification, evidence documentation, and incident response recommendations.

## Objectives

- **Email Header Analysis:** Examine raw email headers and assess authentication results, including SPF, DKIM, and DMARC.
- **URL Analysis:** Identify suspicious URLs, examine hostname structures, and recognise domain impersonation and typosquatting techniques.
- **Threat Intelligence Extraction:** Identify, document, and safely defang relevant Indicators of Compromise (IOCs).
- **Threat Hunting:** Develop Kusto Query Language (KQL) queries to support the identification of related phishing activity across SIEM log sources.
- **Incident Response:** Recommend appropriate containment, investigation, and remediation actions to reduce organisational risk.

## Scenario

An employee in a simulated enterprise environment receives an urgent administrative notification claiming that their Microsoft 365 account password will expire within 24 hours. The message threatens mailbox access restrictions and encourages the recipient to follow an embedded link to maintain account access.

Acting as a Junior SOC Analyst, I examine the available email evidence to assess the legitimacy of the message, identify suspicious characteristics, extract potential IOCs, and recommend appropriate response measures.

The exercise uses synthetic email evidence for educational purposes and does not involve a live phishing campaign or an actual compromised enterprise environment.

## Repository Structure

```text
Phishing-Email-Analysis/
├── README.md
├── sample-email
├── email-header-analysis.md
├── email-analysis.md
└── Indicators-of-compromise.md
```

## Lessons Learned

This investigation highlights the importance of combining email authentication checks, URL analysis, threat intelligence, and proactive threat hunting when responding to suspected phishing activity.

- **Email Authentication and Defence-in-Depth:** SPF, DKIM, and DMARC provide complementary mechanisms for email authentication and domain protection. A strict DMARC policy, such as `p=reject`, can help prevent unauthorised messages from successfully impersonating an organisation's authenticated domain. However, these controls do not automatically prevent attackers from registering look-alike domains. Additional email security controls, domain monitoring, and user awareness remain important.

- **The Danger of Typosquatting:** Attackers may use domains that closely resemble legitimate brands to deceive recipients. Analysing the hostname and identifying its registrable domain is essential when assessing suspicious URLs. Familiar brand names appearing within a URL do not automatically establish that the destination is legitimate.

- **Proactive Threat Hunting Through SIEM:** Investigating a reported phishing email should extend beyond the original recipient. SIEM queries can help analysts search available email, authentication, and endpoint telemetry for related activity, including other recipients, suspicious URLs, and potentially compromised accounts.

- **Incident Response and Automation:** Automating repetitive triage activities, such as URL defanging, reputation checks, and IOC extraction, can improve investigation efficiency. However, automated results should be validated by an analyst before containment or remediation decisions are made.

## Tools and Technologies

- **Email Header Analysis:** Examination of email routing information and authentication results.
- **CyberChef:** Used to support decoding, data transformation, and URL analysis where applicable.
- **WHOIS:** Used to investigate domain registration information and assess available domain history where applicable.
- **Kusto Query Language (KQL):** Used to develop SIEM hunting queries for identifying potentially related phishing activity.
- **ChatGPT (AI Engineering Assistant):** Used to assist in generating synthetic email evidence and supporting the development of the educational scenario. The generated evidence is not presented as a real-world phishing sample.
- **GitHub Markdown:** Used for investigation documentation, evidence organisation, and portfolio presentation.

## Lab Workflow

1. **Evidence Collection (`sample-email`):** Examine the synthetic phishing email sample, including available email headers and message content.

2. **Email Authentication Analysis (`email-header-analysis.md`):** Inspect email routing information and assess SPF, DKIM, and DMARC results. Simulated authentication results are distinguished from independently verified live DNS or cryptographic validation.

3. **Email Content Analysis (`email-analysis.md`):** Examine the message's social engineering techniques, suspicious hyperlinks, and potential domain impersonation.

4. **Threat Intelligence Registration (`Indicators-of-compromise.md`):** Document relevant IOCs in a structured and safely defanged format, alongside KQL detection query examples.

5. **Detection and Response Recommendations:** Develop hunting strategies and recommend appropriate containment, investigation, and remediation actions based on the available evidence.

## Project Status

**Completed — Simulated phishing email investigation and technical documentation.**

The project demonstrates email triage, header analysis, URL investigation, IOC documentation, and the development of SIEM hunting queries.

The investigation uses synthetic evidence and simulated enterprise scenarios. No live phishing campaign, production SIEM deployment, or actual organisational remediation is claimed.
