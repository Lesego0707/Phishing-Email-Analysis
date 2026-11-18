# Indicators of Compromise (IOC) Register

This register documents the indicators identified during a simulated phishing email investigation. It records suspicious email and network characteristics, explains why they may be relevant, and includes basic KQL query examples to illustrate how an analyst could search for related activity in security data.

The indicators are based on synthetic evidence created for this exercise. They have not been confirmed as indicators from a real-world phishing campaign.

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

## 3. Basic KQL Query Examples

The following query examples use Microsoft Sentinel and Microsoft Defender XDR table structures to demonstrate how security-related email and endpoint data could be searched for the indicators identified during this investigation.

These queries were written for learning and documentation purposes. They have not been executed against ingested security data or deployed as detection rules in a SIEM environment.

### A. Email Sender Hunt

Search email records for messages containing the claimed sender address or envelope sender address.

```kusto
EmailEvents
| where SenderFromAddress =~ "security@microsoft.com"
    or SenderMailFromAddress =~ "security@microsoft.com"
| project Timestamp, NetworkMessageId, SenderFromAddress,
          SenderMailFromAddress, RecipientEmailAddress,
          Subject, DeliveryAction
| order by Timestamp desc
```
> **Analyst note:** Identifies messages using the claimed sender or envelope sender address. Matching results do not independently prove spoofing or malicious activity.

### B. Email URL Hunt

Search endpoint network records for activity involving the suspicious domain.

```kusto
EmailUrlInfo
| where Url contains "microsoft-security-alert.xyz"
| project Timestamp, NetworkMessageId, Url
| order by Timestamp desc
```
> **Analyst note:** Searches email URL telemetry for references to the suspicious domain. Correlate matching NetworkMessageId values with EmailEvents to investigate recipients and message delivery details.

### C. Endpoint Network Activity Hunt

Search endpoint network records for activity involving the suspicious domain.

```kusto
DeviceNetworkEvents
| where RemoteUrl contains "microsoft-security-alert.xyz"
| project Timestamp, DeviceName,
          InitiatingProcessAccountName,
          RemoteUrl, RemoteIP, LocalIP
| order by Timestamp desc
```
> **Analyst note:** Searches endpoint network telemetry for activity involving the suspicious domain. Results depend on endpoint visibility and whether the destination hostname is recorded in RemoteUrl.

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
- The KQL query examples are for learning and documentation purposes. They have not been executed against live or ingested SIEM data, and their results have not been validated.
- Query execution depends on the relevant tables, field names, data availability, and schema in the target environment.

## 6. Analyst Conclusion

This investigation allowed me to practise identifying and documenting suspicious email and network indicators using synthetic phishing evidence. I examined sender information, email authentication results, suspicious domains, and URLs to understand why the email could be considered suspicious.

I also wrote basic KQL query examples to explore how these indicators could be used to search security-related data in a future investigation. Although I have not yet executed these queries in a SIEM environment, this exercise helped me understand the relationship between IOC documentation, security data, and query-based investigation.
