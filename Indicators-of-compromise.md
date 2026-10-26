# Indicators of Compromise (IOC) Register

## 1. Purpose

This document records potential and verified indicators relevant to case PHISH-001.

In a SOC investigation, IOCs are observable artifacts that may help identify malicious activity, such as suspicious domains, URLs, IP addresses, file hashes, or email sender infrastructure.

Suspicious wording and social-engineering techniques are useful evidence, but they are not necessarily technical IOCs.

## 2. Case Information

| Field | Details |
|---|---|
| Case ID | PHISH-001 |
| Investigation Type | Phishing Email Analysis |
| Evidence Source | Simulated email |
| Current Status | Preliminary review |
| IOC Verification | No malicious technical indicators verified |

## 3. IOC Register

| Indicator Type | Observed Value | Assessment | Status |
|---|---|---|---|
| Sender address | `security@example.invalid` | Placeholder sender identity | Training data only |
| Reply-To address | `support@example.invalid` | Different from sender address; not proof of malicious activity | Training data only |
| Domain | `example.invalid` | Reserved invalid example domain | Not a malicious IOC |
| URL | Not provided | Cannot assess destination or reputation | Not available |
| IP address | Not provided | No sending IP can be established | Not available |
| File hash | Not provided | No attachment available for hashing | Not available |
| Attachment | Not provided | No file analysis possible | Not available |

**Important:** The example addresses and domain are included only to support a safe training scenario. They must not be reported as real attacker infrastructure or malicious IOCs.

## 4. Suspicious Email Characteristics

The following characteristics support further investigation but are not verified technical IOCs.

| Characteristic | Why It Matters |
|---|---|
| Urgent deadline | May pressure a recipient into acting without verification. |
| Threat of account suspension | Uses fear to influence user behaviour. |
| Request to verify account details | May be an attempt to obtain credentials or sensitive information. |
| Claimed Microsoft identity | Requires verification of the sender's actual identity. |

## 5. IOC Verification Workflow

For an authorized investigation involving a genuine suspicious email:

1. Preserve the original email and its full headers.
2. Extract actual sender, Reply-To, sending IP, URLs, and attachment metadata where available.
3. Review SPF, DKIM, and DMARC results.
4. Check appropriate domains, IPs, URLs, or file hashes using approved security tools.
5. Correlate results with other evidence before classifying an indicator as malicious.
6. Record the source, timestamp, analysis result, and confidence level for each finding.
7. Share or block indicators only in accordance with organizational procedures.

## 6. Investigation Limitations

This case uses a self-created simulated email. It does not contain a real sender IP, a live destination URL, an attachment, or a file hash.

No VirusTotal detections, DNS findings, authentication results, or external threat intelligence findings have been established for this case.

These fields should be updated only when genuine, appropriate evidence becomes available.

## 7. Conclusion

The email contains suspicious social-engineering characteristics, but no malicious technical IOC has been verified.

This distinction is important in SOC work: indicators must be supported by evidence, and a suspicious email should not be attributed to an attacker without sufficient investigation.

The IOC register will be updated if additional evidence becomes available.
