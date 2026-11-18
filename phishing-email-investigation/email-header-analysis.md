# Email Header & Authentication Analysis

This phase of the investigation focuses on examining the available email header information to assess sender authenticity, evaluate email authentication results, and identify potentially suspicious mail infrastructure.

The analysis uses synthetic email evidence created for this educational exercise. Authentication results and infrastructure indicators are simulated and have not been independently verified against Microsoft's live email infrastructure.

## 1. Authentication Summary (SPF, DKIM, DMARC)

The simulated email authentication results indicate failures across all three core email authentication mechanisms.

| Protocol | Status | Analyst Findings & Implications |
|---|---|---|
| **SPF** | ❌ **FAIL (Simulated)** | The synthetic `Received-SPF` result indicates that the sending IP address (`198.51.100.12`) is not authorised to send email on behalf of the claimed domain. The IP belongs to the documentation-only TEST-NET-2 range and is not a real Microsoft or attacker infrastructure address. |
| **DKIM** | ❌ **FAIL (Simulated)** | The simulated result indicates that DKIM authentication failed. In a real investigation, the signature and authentication details would need to be examined to determine the reason for the failure. No independent DKIM verification was performed for this exercise. |
| **DMARC** | ❌ **FAIL (Simulated)** | The simulated DMARC result indicates that neither SPF nor DKIM produced a passing, aligned authentication result for the visible From domain. DMARC requires at least one of these mechanisms to pass and align with the From domain. The scenario assumes a hypothetical `p=reject` policy, but no live Microsoft DMARC policy lookup was performed. |

**Analyst Observation:**

All three email authentication checks are shown as failed in the simulated results. This made me question whether the email was genuinely sent by Microsoft. I learned that these failures are important warning signs, but they should not be used on their own to determine whether an email is malicious. They need to be considered together with the sender details, Reply-To address, message content, and other available evidence.

## 2. Mail Envelope & Routing Breakdown

The following indicators are taken from the synthetic email sample.

- **Claimed Sender (`From:`):** `Microsoft Account Team <security@microsoft.com>`
-  **Analysis:** The visible sender address claims to represent Microsoft. This identity should not be trusted without validating the authentication results and other available evidence.

- **Reported Sending Host (`Received:`):** `mail.microsoft-security-alert.xyz`
  - **Analysis:** The synthetic routing information identifies a mail host using a domain that resembles Microsoft's branding. The registrable domain is `microsoft-security-alert.xyz`, not `microsoft.com`. This is consistent with a possible brand-impersonation technique.

- **Source IP Address:** `198.51.100.12`
  - **Analysis:** This is a documentation-only IPv4 address within the TEST-NET-2 range, reserved for examples and documentation under RFC 5737. It is not a real public attacker IP and cannot be used to identify or geolocate actual malicious infrastructure.
- **Reply-To Address:** `support@microsoft-security-alert.xyz`
- **Analysis:** The Reply-To address differs from the claimed Microsoft sender domain. If the recipient replies, the email client may direct the response to the alternative address, potentially exposing information to an unauthorised party.

**Analyst Observation:**

What stood out to me was that the email claimed to come from Microsoft, but the reported sending host and Reply-To address used a different domain. This raised my suspicion that the sender was impersonating Microsoft. The different Reply-To address was particularly concerning because a recipient replying to the email could be communicating with an address outside Microsoft's domain.

## 3. Infrastructure Triage Methodology (Hypothetical)

Although live infrastructure investigation was outside the scope of this synthetic exercise, the following methodology outlines the checks a SOC analyst would perform to assess suspicious email infrastructure in a real-world investigation.

### 3.1 Domain Registration Analysis (WHOIS/RDAP)
- Examine domain registration and creation dates.
- Identify the registrar and available registration information.
- Investigate whether the domain was recently registered.
- Assess domain age alongside other indicators rather than treating recent registration as proof of malicious activity.

### 3.2 DNS and Hosting Analysis
- Examine A, MX, NS, and TXT records where available.
- Identify the mail hosting provider and associated infrastructure.
- Check whether SPF and DMARC records exist and assess their configuration.
- Compare the findings against the claimed organisation's legitimate domains.

### 3.3 ASN and IP Reputation Analysis
- Identify the Autonomous System Number (ASN) associated with a real, routable source IP.
- Examine the network provider and hosting organisation.
- Check reputable threat intelligence sources for previous reports of suspicious activity.
- Compare the results against known legitimate infrastructure.

**Technical limitation:** The synthetic IP address `198.51.100.12` is reserved for documentation purposes. Therefore, meaningful public infrastructure or ASN attribution cannot be established from this address.

### 3.4 Threat Intelligence Correlation
- Search available threat intelligence platforms for domain and IP reputation.
- Check for previous phishing or malware associations.
- Correlate infrastructure findings with the suspicious email content and authentication results.

   **Note:** The synthetic IP address `198.51.100.12` is reserved for documentation, so meaningful public infrastructure or ASN attribution cannot be established from it.

## 4. Analyst Conclusion

Based on the evidence presented in this simulated investigation, I consider the email suspicious and consistent with a phishing attempt.

The main reasons for my assessment are the simulated authentication failures, the Microsoft sender identity, the suspicious domain used in the reported sending host, the different Reply-To address, and the urgency created by the account-suspension message.

These findings raised concerns that the email could be intended to deceive recipients and direct them to an unauthorised source. However, because the evidence is synthetic and the sending infrastructure was not independently verified, I cannot confirm an actual phishing campaign or identify a real attacker.

This investigation helped me understand how different email indicators can support an assessment, and why it is important to explain the evidence behind a conclusion rather than rely on a single suspicious detail.

## 5. Lessons Learned

Through this exercise, I learned how to read email header information more carefully and why the visible sender address alone cannot be relied upon to establish whether an email is legitimate.

I gained a better understanding of SPF, DKIM, and DMARC, and how their authentication results can help assess sender authenticity. I also learned that authentication failures are warning signs that need to be considered alongside other evidence rather than treated as automatic proof of phishing.

Examining the From, Reply-To, and Received fields helped me understand how email identities and routing information can reveal inconsistencies. I learned why the Reply-To address is particularly important, as it may direct a response somewhere different from the address displayed to the recipient.

Another important lesson was understanding the limitations of the evidence. Since this investigation used synthetic headers and a documentation-only IP address, I could assess the indicators presented in the scenario but could not independently verify real sending infrastructure or attribute activity to an actual source.

This exercise taught me to be more careful when interpreting technical evidence, to distinguish simulated results from independently verified findings, and to avoid making conclusions beyond what the available information supports.

