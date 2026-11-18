 Phishing-Email-Analysis
 
## Project Overview
The investigation focuses on a credential-harvesting attempt impersonating a Microsoft 365 administrative security alert. The exercise involves examining raw email headers, analysing social engineering techniques, identifying suspicious URLs, extracting Indicators of Compromise (IOCs), and drafting basic Kusto Query Language (KQL) query examples for potential security investigations.

The project demonstrates a structured approach to phishing email analysis, evidence documentation, and security response recommendations.

## Objectives

- **Email Header Analysis:** Examine raw email headers and assess authentication results, including SPF, DKIM, and DMARC.
- **URL Analysis:** Identify suspicious URLs, examine hostname structures, and recognise domain impersonation and typosquatting techniques.
- **IOC Identification:** Identify, document, and safely defang relevant Indicators of Compromise (IOCs).
- **Basic KQL Practice:** Develop introductory KQL query examples to demonstrate how security-related data could be filtered and reviewed during an investigation.
- **Incident Response Awareness:** Identify appropriate containment, investigation, and remediation recommendations based on the available evidence.

## Scenario

An employee in a simulated enterprise environment receives an urgent administrative notification claiming that their Microsoft 365 account password will expire within 24 hours. The message threatens mailbox access restrictions and encourages the recipient to follow an embedded link to maintain account access.

Acting as a Junior SOC Analyst, I examine the available email evidence to assess the legitimacy of the message, identify suspicious characteristics, extract potential IOCs, and recommend appropriate response measures.

The exercise uses synthetic email evidence for educational purposes and does not involve a live phishing campaign or an actual compromised enterprise environment.

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

Through this investigation, I learned that analysing a phishing email involves more than looking at the sender's address or the message content. I need to examine different pieces of evidence together before deciding whether an email is suspicious.

I learned how to review email headers and interpret SPF, DKIM, and DMARC authentication results. I also gained a better understanding of why the Reply-To address matters, especially when it differs from the sender's address and directs replies to a suspicious domain.

Another important lesson was recognising domain impersonation. I learned that a familiar company name appearing in a URL does not mean the website is legitimate. Examining the actual hostname helped me identify suspicious domain characteristics that could easily be overlooked.

I also gained practical experience identifying, extracting, and safely documenting Indicators of Compromise (IOCs). This helped me understand how information collected during an investigation can be organised for further security analysis.

I also gained introductory experience writing basic KQL queries to search and filter security-related data. This helped me understand how queries can be used to identify information that may be relevant to an investigation. I am still developing my KQL skills and look forward to applying them in a practical SIEM environment.

Most importantly, I learned that individual warning signs should not be considered in isolation. A stronger assessment comes from combining email authentication results, sender information, suspicious links, and other available evidence. I also learned to distinguish between what the evidence suggests and what I can actually confirm.

## Tools and Technologies

- **Email Header Analysis:** Examination of email routing information and authentication results.
- **CyberChef:** Used to support decoding, data transformation, and URL analysis where applicable.
- **WHOIS:** Used to investigate domain registration information and available registration details where applicable.
- **Kusto Query Language (KQL):** Used to write basic query examples for filtering and reviewing security-related data. 
- **ChatGPT:** Used to assist with generating synthetic email evidence and developing the educational scenario.


## Lab Workflow

1. **Evidence Collection (`sample-email`):** Examine the synthetic phishing email sample, including available email headers and message content.

2. **Email Authentication Analysis (`email-header-analysis.md`):** Inspect email routing information and assess SPF, DKIM, and DMARC results. Simulated authentication results are distinguished from independently verified live DNS or cryptographic validation.

3. **Email Content Analysis (`email-analysis.md`):** Examine the message's social engineering techniques, suspicious hyperlinks, and potential domain impersonation.

4. **IOC Identification and Documentation (`Indicators-of-compromise.md`):** Identify relevant indicators, document them in a structured and safely defanged format, and include basic KQL query examples for learning purposes.

5. **Security Recommendations:** Document suggested investigation, containment, and remediation steps that an organisation could consider if similar activity were identified.


## Project Status

**Completed — Simulated phishing email investigation and technical documentation.**

The project demonstrates introductory email analysis, email header examination, URL investigation, IOC identification and documentation, and basic KQL query development.
