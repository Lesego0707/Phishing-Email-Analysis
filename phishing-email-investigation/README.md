# Phishing-Email-Analysis

## Project Overview

This project documents a simulated phishing email investigation based on a message impersonating a Microsoft 365 administrative security alert.

For this exercise, I approached the evidence from the perspective of a beginner SOC analyst. I examined the available email headers, reviewed the message for social engineering techniques, identified suspicious URLs, documented potential Indicators of Compromise (IOCs), and wrote basic KQL query examples for learning purposes.

The project helped me develop a better understanding of phishing email analysis, evidence documentation, and how an analyst can assess suspicious activity without making conclusions beyond the available evidence.

## Objectives

- **Email Header Analysis:** Examine email headers and understand SPF, DKIM, and DMARC authentication results.
- **URL Analysis:** Identify suspicious URLs and recognise domain impersonation techniques.
- **IOC Identification:** Extract, document, and safely defang potential Indicators of Compromise.
- **Basic KQL Practice:** Write introductory KQL query examples to understand how security-related data can be filtered and reviewed.
- **Incident Response Awareness:** Identify appropriate investigation, containment, and remediation recommendations based on the available evidence.

## Scenario

An employee in a simulated enterprise environment receives an urgent administrative notification claiming that their Microsoft 365 account password will expire within 24 hours. The message threatens mailbox access restrictions and encourages the recipient to follow an embedded link to maintain account access.

For this exercise, I examine the available email evidence to assess whether the message is suspicious, identify potential warning signs, document relevant indicators, and recommend appropriate response measures.

The exercise uses synthetic email evidence for educational purposes. It does not represent a live phishing campaign or an actual compromised enterprise environment.

## Repository Structure

```text
Phishing-Email-Analysis/
│
├── README.md
│
└── phishing-email-investigation/
    ├── sample-email/
    ├── email-header-analysis.md
    ├── email-analysis.md
    └── Indicators-of-compromise.md

```

## Lessons Learned

Through this project, I learned that investigating a phishing email involves looking beyond the sender's name and the message itself. I needed to examine different pieces of evidence to understand why the email was suspicious.

I learned how SPF, DKIM, and DMARC authentication results can help assess email authenticity. I also discovered why a different Reply-To address and a suspicious sending domain deserve attention when reviewing an email.

Examining the message content helped me recognise how urgency, fear, and the use of a familiar company's name can influence someone into acting without checking whether a message is genuine.

I also learned how to identify and document potential IOCs in a structured format. This helped me understand how information collected during an investigation can be organised for further analysis.

Writing basic KQL query examples introduced me to how queries can be used to filter and review security-related data. I am still developing this skill and have not yet applied these queries in a practical SIEM environment.

Most importantly, I learned not to jump to conclusions based on one suspicious indicator. The findings need to be considered together, and I must be able to explain what the available evidence supports and what I cannot confirm.

```

## Tools and Technologies

- **Email Header Analysis:** Examination of email routing information and authentication results.
- **CyberChef:** Used to support decoding and data transformation where applicable.
- **WHOIS:** Used to investigate domain registration information where applicable.
- **Kusto Query Language (KQL):** Used to write basic query examples for filtering and reviewing security-related data. These examples were created for learning purposes and were not executed in a SIEM environment.
- **ChatGPT:** Used to assist with generating synthetic email evidence and developing the educational scenario.

```

## Lab Workflow

1. **Evidence Collection (`sample-email`):** Examine the synthetic phishing email sample, including available email headers and message content.

2. **Email Authentication Analysis (`email-header-analysis.md`):** Review email routing information and assess the simulated SPF, DKIM, and DMARC results.

3. **Email Content Analysis (`email-analysis.md`):** Examine the message's social engineering techniques, suspicious hyperlinks, and potential domain impersonation.

4. **IOC Identification and Documentation (`Indicators-of-compromise.md`):** Identify potential indicators, document them in a structured and safely defanged format, and include basic KQL query examples.

5. **Security Recommendations:** Document appropriate investigation, containment, and remediation steps that could be considered in a similar real-world situation.
   
```
## Project Status

**Completed — Simulated phishing email investigation and technical documentation.**

The project demonstrates introductory email analysis, email header examination, URL investigation, IOC identification and documentation, and basic KQL query development.
