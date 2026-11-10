# Indicators of Compromise (IOC) Register

This register documents the indicators identified during a **simulated phishing email investigation**. It records suspicious email and network characteristics, explains their relevance, and provides example detection queries for security monitoring.

The indicators are based on the synthetic evidence used in this exercise. They have not been confirmed as indicators from a real-world phishing campaign.

## Defanging Policy

Network indicators are defanged to reduce the risk of accidental clicks or connections. For example:

- `http` becomes `hxxp`
- `.` becomes `[.]`

**Important:** Defanged indicators are used for documentation. Detection queries that search real security logs must use the original, un-defanged values because logs normally record the original URLs, domains and IP addresses.

---

## 1. Network and Infrastructure Indicators

| Indicator Type | Value (Defanged) | Context / Association | Suggested Defensive Action |
|---|---|---|---|
| Source IP | `198[.]51[.]100[.]12` | Synthetic source IP used in the exercise. This address belongs to the TEST-NET-2 documentation range and is not a confirmed attacker IP. | Do not block as a real threat indicator. Replace with a validated source IP if conducting a real investigation. |
| Suspicious Domain | `microsoft-security-alert[.]xyz` | Look-alike domain that does not belong to the official `microsoft.com` domain. | Investigate domain reputation and DNS activity. Consider blocking only after validation. |
| Reported Mail Hostname | `mail[.]microsoft-security-alert[.]xyz` | Hostname recorded in the simulated email-routing evidence. Its presence should be assessed alongside trusted Received headers. | Review email gateway and DNS logs. Consider a block after validating the evidence. |
| Suspicious URL | `hxxp://microsoft-security-alert[.]xyz` | URL recorded in the email body. It uses HTTP and a domain that resembles a Microsoft security notification domain. | Do not visit the URL. Investigate and consider blocking through web filtering after validation. |

**Evidence limitation:** The source IP is reserved for documentation, and the hostname and domain are part of a simulated scenario. They should not be presented as verified attacker infrastructure.

---

## 2. Behavioral and Email Indicators

| Indicator Type | Threat Value | Analyst Notes |
|---|---|---|
| Claimed Display Name | `Microsoft Account Team` | Display name used to create an impression of legitimacy and authority. Display names can be chosen by senders and do not establish identity. |
| Claimed Sender Address | `security@microsoft.com` | Address shown in the From field. It requires authentication and header analysis before concluding that it was spoofed. |
| Reply-To Address | `support@microsoft-security-alert.xyz` | Different from the claimed sender domain. This discrepancy is suspicious and could redirect replies to an unrelated domain. |
| Subject Keyword | `Urgent: Your account will be suspended` | Creates urgency and fear to encourage the recipient to act without verifying the message. |

These characteristics should be assessed together. A suspicious subject line or display name alone does not prove that an email is malicious.

---

## 3. SIEM Detection and Threat Hunting Queries

The following are example Microsoft Sentinel / Microsoft Defender XDR hunting queries. They are provided as detection logic for a lab exercise; they have not been deployed or tested against a live enterprise environment.

### A. Email Sender Hunt

Search for messages using the claimed sender address or envelope sender address.

```kql
EmailEvents
| where SenderFromAddress =~ "security@microsoft.com"
    or SenderMailFromAddress =~ "security@microsoft.com"
| project Timestamp, NetworkMessageId, SenderFromAddress,
          SenderMailFromAddress, RecipientEmailAddress,
          Subject, DeliveryAction
| order by Timestamp desc
```

**Analyst note:** This query identifies messages using the claimed address. It does not prove spoofing or malicious activity. Review authentication results, sender infrastructure and message context before reaching a conclusion.

### B. Email URL Hunt

Search email URL records for the suspicious domain.

```kql
EmailUrlInfo
| where Url contains "microsoft-security-alert.xyz"
| project Timestamp, NetworkMessageId, Url
| order by Timestamp desc
```

**Analyst note:** Review matching messages and correlate their `NetworkMessageId` values with email event records to identify recipients and delivery details.

### C. Endpoint Network Activity Hunt

Search endpoint network telemetry for connections involving the suspicious domain.

```kql
DeviceNetworkEvents
| where RemoteUrl contains "microsoft-security-alert.xyz"
| project Timestamp, DeviceName, InitiatingProcessAccountName,
          RemoteUrl, RemoteIP, LocalIP
| order by Timestamp desc
```

**Analyst note:** This query can help identify endpoints with network activity involving the domain, provided the relevant endpoint telemetry is available and the domain is recorded in `RemoteUrl`.

---

## 4. Recommended Defensive Response

If these indicators were encountered in a real investigation, a SOC analyst could recommend the following actions:

1. **Validate the evidence:** Confirm the original message headers, sender authentication results, URL and routing information.
2. **Identify affected recipients:** Search email telemetry for other recipients who received the same or similar messages.
3. **Investigate user interaction:** Review available URL-click, proxy, DNS and endpoint telemetry to determine whether users interacted with the suspicious link.
4. **Contain the threat:** Recommend quarantining confirmed malicious messages and blocking validated malicious domains or URLs through approved security controls.
5. **Escalate where necessary:** If credentials may have been submitted, follow the organisation's account-compromise response procedure.
6. **Document findings:** Record the evidence, investigation steps, affected users, conclusions and recommended remediation.

## 5. Project Limitations

- The email sample and scenario are synthetic.
- The source IP `198.51.100.12` is reserved for documentation and is not a verified malicious IP.
- The domain and URL are suspicious scenario indicators, not confirmed live attacker infrastructure.
- No live URL was visited and no credentials were collected.
- The KQL queries are examples and have not been run against a production SIEM.
- Query results depend on the relevant Microsoft Defender or Sentinel tables being available and populated.

## 6. Analyst Conclusion

This exercise demonstrates how a SOC analyst can extract and document email-related indicators, assess suspicious sender and URL characteristics, and develop example SIEM queries to support threat hunting.

The investigation highlights the importance of validating evidence before classifying an indicator as malicious or recommending containment actions. Accurate documentation and evidence-based conclusions are essential parts of effective security operations.
