# Email Header & Authentication Analysis

This phase of the investigation focuses on examining the available email header information to assess sender authenticity, evaluate email authentication results, and identify potentially suspicious mail infrastructure.

The analysis uses synthetic email evidence created for this educational exercise. Authentication results and infrastructure indicators are simulated and have not been independently verified against Microsoft's live email infrastructure.

## 1. Authentication Summary (SPF, DKIM, DMARC)

The simulated email authentication results indicate failures across all three core email authentication mechanisms.

| Protocol | Status | Analyst Findings & Implications |
|---|---|---|
| **SPF** | ❌ **FAIL (Simulated)** | The synthetic `Received-SPF` result indicates that the sending IP address (`198.51.100.12`) is not authorised to send email on behalf of the claimed domain. The IP belongs to the documentation-only TEST-NET-2 range and is not a real Microsoft or attacker infrastructure address. |
| **DKIM** | ❌ **FAIL (Simulated)** | The synthetic authentication result indicates that a valid DKIM signature could not be verified. This may occur when a signature is missing, invalid, or fails cryptographic verification. It does not independently prove that the message was modified in transit. |
| **DMARC** | ❌ **FAIL (Simulated)** | The simulated DMARC result indicates that neither SPF nor DKIM produced a passing, aligned authentication result for the visible From domain. DMARC requires at least one of these mechanisms to pass and align with the From domain. The scenario assumes a hypothetical `p=reject` policy, but no live Microsoft DMARC policy lookup was performed. |

**Analyst Observation:**

The combined authentication failures represent a significant warning sign in this simulated investigation. However, authentication results should be interpreted alongside the sender address, reply-to information, message content, and available routing evidence before reaching a final verdict.

A DMARC rejection policy instructs receiving mail systems to reject messages that fail DMARC evaluation, subject to receiver handling and local policy. It does not guarantee that every unauthenticated or look-alike message will be blocked.

## 2. Mail Envelope & Routing Breakdown

The following indicators are taken from the synthetic email sample.

- **Claimed Sender (`From:`):** `Microsoft Account Team <security@microsoft.com>`
  - **Analysis:** The visible sender address claims to represent Microsoft. This identity should not be trusted without validating the authentication results and other available evidence.

- **Reported Sending Host (`Received:`):** `mail.microsoft-security-alert.xyz`
  - **Analysis:** The synthetic routing information identifies a mail host using a domain that resembles Microsoft's branding. The registrable domain is `microsoft-security-alert.xyz`, not `microsoft.com`. This is consistent with a possible brand-impersonation technique.

- **Source IP Address:** `198.51.100.12`
  - **Analysis:** This is a documentation-only IPv4 address within the TEST-NET-2 range, reserved for examples and documentation under RFC 5737. It is not a real public attacker IP and cannot be used to identify or geolocate actual malicious infrastructure.

- **Reply-To Address:** `support@microsoft-security-alert.xyz`
  - **Analysis:** The Reply-To address differs from the claimed Microsoft sender domain. If the recipient replies, the email client may direct the response to the alternative address, potentially exposing information to an unauthorised party.

**Analyst Observation:**

The mismatch between the visible sender identity, reported sending host, and Reply-To address raises suspicion of brand impersonation and possible credential-harvesting activity.

However, Received headers must be interpreted carefully. An analyst should identify trusted mail servers and establish which systems added the routing information. Individual Received headers can be forged before a message enters trusted mail infrastructure.

## 3. Infrastructure Triage Methodology (Hypothetical — No Live Lookup Performed)

As this exercise uses synthetic infrastructure indicators, no live domain registration, DNS, IP reputation, or ASN investigation was performed.

In a real SOC investigation, the following checks would help establish whether the reported infrastructure is associated with malicious activity.

1. **Domain Registration Analysis (WHOIS/RDAP):**
   - Examine domain registration and creation dates.
   - Identify the registrar and available registration information.
   - Investigate whether the domain was recently registered.
   - Assess domain age alongside other indicators rather than treating recent registration as proof of malicious activity.

2. **DNS and Hosting Analysis:**
   - Examine A, MX, NS, and TXT records where available.
   - Identify the mail hosting provider and associated infrastructure.
   - Check whether SPF and DMARC records exist and assess their configuration.
   - Compare the findings against the claimed organisation's legitimate domains.

3. **ASN and IP Reputation Analysis:**
   - Identify the Autonomous System Number (ASN) associated with a real, routable source IP.
   - Examine the network provider and hosting organisation.
   - Check reputable threat intelligence sources for previous reports of suspicious activity.
   - Compare the results against known legitimate infrastructure.

   **Note:** The synthetic IP address `198.51.100.12` is reserved for documentation, so meaningful public infrastructure or ASN attribution cannot be established from it.

4. **Threat Intelligence Correlation:**
   - Search available threat intelligence platforms for domain and IP reputation.
   - Check for previous phishing or malware associations.
   - Correlate infrastructure findings with the suspicious email content and authentication results.

## 4. Analyst Conclusion

The simulated email exhibits several characteristics consistent with a phishing attempt:

- Failed simulated SPF, DKIM, and DMARC authentication results.
- A visible sender address claiming to represent Microsoft.
- A reported sending host using a brand-imitating domain.
- A Reply-To address pointing to a different domain.
- A hypothetical account-suspension threat designed to create urgency.

Taken together, these indicators support classifying the message as **suspected phishing within the simulated exercise**.

The findings are based on synthetic evidence and should not be interpreted as proof of a real Microsoft security incident or actual attacker infrastructure.
