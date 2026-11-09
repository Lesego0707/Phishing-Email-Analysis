#  Email Header & Authentication Analysis

In this phase, I extracted and evaluated the network routing data from the raw email file to verify sender authenticity and track the true origin of the message.

## 1. Authentication Summary (SPF, DKIM, DMARC)

The email records an absolute failure across all three core defensive verification checks:

| Protocol | Status | Analyst Findings & Implications |
| :--- | :--- | :--- |
| **SPF** | ❌ **FAIL** | The `Received-SPF` record shows that the sending server IP address (`198.51.100.12`) is **not** authorized by Microsoft's official DNS records to send emails on behalf of `microsoft.com`. |
| **DKIM** | ❌ **FAIL** | The message did not contain a valid cryptographic signature from `microsoft.com`, indicating the email body was either modified in transit or created by an unauthorized mail platform. |
| **DMARC** | ❌ **FAIL** | Because both SPF and DKIM failed to align with the visible domain, DMARC failed. The official policy of the spoofed domain is `p=REJECT`, meaning this email should have been blocked before delivery. |

---

## 2. Mail Envelope & Routing Breakdown

*   **Claimed Sender (`From:`):** `Microsoft Account Team <security@microsoft.com>`
    *   *Analysis:* Visual spoofing designed to abuse user trust by impersonating official administrative infrastructure.
*   **True Host Domain (`Received:`):** `mail.microsoft-security-alert.xyz`
    *   *Analysis:* The true domain from which the mail server initiated connection. This is a look-alike domain (typosquatting) registered by the attacker.
*   **Source IP Address:** `198.51.100.12`
    *   *Analysis:* The public IPv4 address of the malicious Mail Transfer Agent (MTA).
*   **Reply-To Path:** `support@microsoft-security-alert.xyz`
    *   *Analysis:* A critical defensive indicator. If the victim manually replies to the alert, the message bypasses Microsoft completely and routes straight back to the attacker's server.

---

## 3. Infrastructure Triage Methodology (Hypothetical — No Live Lookup Performed)

As this is a synthetic training scenario, the domain itself cannot be queried live — below is the triage an analyst would perform and the indicators that would typically confirm malicious infrastructure.

1. **Domain Age:** A WHOIS lookup would typically show a newly registered domain (often less than 48 hours old). Legitimate organizational security alerts do not originate from brand-new, generic domains — a young domain age is a strong red flag for attacker-controlled infrastructure.

2. **ASN Mapping:** A lookup of the IP's Autonomous System Number (ASN) would typically show it does not route back to known Microsoft data centers, which would further confirm the infrastructure is unrelated to the legitimate brand being spoofed.
