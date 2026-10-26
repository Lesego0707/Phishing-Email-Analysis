# Phishing Email Analysis

## 1. Case Details

| Field | Details |
|---|---|
| Case ID | PHISH-001 |
| Investigation Type | Email Threat Analysis |
| Email Subject | Urgent: Your account will be suspended |
| Claimed Brand | Microsoft 365 |
| Evidence Type | Simulated email content |
| Investigation Status | Initial analysis |

## 2. Objective

The objective is to assess the supplied email for characteristics associated with phishing, document the available evidence, and identify further investigation steps required to establish whether the message is malicious.

## 3. Indicator Analysis

### A. Sender Address

**Observed value:** `security@example.invalid`

**Analysis:** The display name claims to represent a Microsoft account security team, but the sender address uses a reserved invalid example domain rather than a verified Microsoft domain.

**Finding:** The claimed sender identity is not established. Because this is a training sample, the address is a placeholder and cannot be used to attribute a real phishing campaign.

### B. Reply-To Address

**Observed value:** `support@example.invalid`

**Analysis:** The Reply-To address is different from the sender address. A mismatch can be suspicious when replies are redirected to an unrelated destination, but different addresses can also be legitimate.

**Finding:** The difference is worth checking, but the simulated addresses alone do not prove malicious intent.

### C. Subject Line

**Observed value:** `Urgent: Your account will be suspended`

**Analysis:** The subject creates urgency and suggests that the recipient could lose access to their account.

**Finding:** This is a potential social-engineering indicator designed to pressure the recipient into acting quickly.

### D. Email Body

**Observed characteristics:**
- Generic greeting: "Dear User"
- A warning about unusual account activity
- A 24-hour deadline
- A threat of account suspension
- A request to verify account details

**Analysis:** These characteristics may be intended to create fear and encourage the recipient to disclose sensitive information or follow an unverified instruction.

**Finding:** The message contains multiple phishing-like characteristics. Further evidence is required before confirming the classification of a real email.

### E. Links and Attachments

**Observed value:** No actual URL or attachment was supplied in the training sample.

**Analysis:** A URL reputation check or attachment analysis cannot be performed without an actual indicator to investigate.

**Finding:** No URL or attachment has been verified as malicious. No indicators should be invented to fill this gap.

## 4. Email Authentication: Further Investigation

For a real email, the following authentication mechanisms should be reviewed where available:

| Mechanism | Purpose |
|---|---|
| SPF | Checks whether the sending server is authorized under the domain's SPF policy. |
| DKIM | Uses a digital signature to help verify message integrity and domain association. |
| DMARC | Applies a domain policy and alignment checks involving SPF and/or DKIM. |

Authentication results must be interpreted in context. A phishing email can pass authentication when sent through an attacker-controlled domain, and a legitimate email can fail authentication because of forwarding or configuration issues.

**Current status:** SPF, DKIM, and DMARC results are unavailable because no real email headers were provided.

## 5. Initial Risk Assessment

**Preliminary risk:** Potentially suspicious.

The urgency, threatened account suspension, and request to verify account details warrant further examination. However, this simulated content does not establish that a real account was targeted or compromised.

For a real incident, severity would depend on evidence such as the destination URL, sender infrastructure, authentication results, whether the recipient interacted with the message, and whether credentials were submitted.

## 6. Recommended SOC Response

1. Preserve the original email and its headers when authorized.
2. Review the sender identity and Reply-To destination.
3. Analyse available URLs and attachments using approved tools.
4. Search for similar messages within the organization's email environment if appropriate access is available.
5. If the message is confirmed malicious, follow established procedures to quarantine or remove it and block verified malicious indicators.
6. If a recipient submitted credentials, escalate promptly and follow the organization's account-compromise response procedures.

## 7. Conclusion

The simulated email contains several characteristics associated with phishing, including urgency, a threatened account suspension, and a request to verify account details.

The available evidence supports classifying the message as suspicious for training purposes, but does not establish the authenticity of a real sender, the presence of a malicious URL, or a successful credential-theft attempt.

Further investigation using genuine email headers and verified indicators would be necessary for a conclusive determination.

## 8. Lessons Learned

This exercise demonstrates the importance of evaluating multiple indicators rather than relying on a single suspicious phrase. It also reinforces the need to distinguish observed facts from assumptions and to document evidence limitations in a security investigation.
