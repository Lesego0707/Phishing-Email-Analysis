# Indicators of Compromise (IOC) Register
This register catalogues the technical data points and threat intelligence collected during the investigation. These indicators can be used by defensive teams to block the threat at the perimeter and hunt for other impacted systems.

## 🛠️ Defanging Policy
To ensure repository safety and prevent accidental clicks, all network indicators below have been **defanged** (e.g., changing `http` to `hxxp` and using brackets `[.]` for periods).

---

## 1. Network & Infrastructure IOCs

| Indicator Type | Value (Defanged) | Context / Association | Suggested Defensive Action |
| :--- | :--- | :--- | :--- |
| **Originating IP** | `198[.]51[.]100[.]12` | Malicious mail transfer agent server used to send the message. | Block at perimeter firewall level. |
| **Malicious Domain** | `microsoft-security-alert[.]xyz` | Look-alike root domain registered by the attacker for typosquatting. | Sinkhole / Block at internal DNS layers. |
| **Mail Hostname** | `mail[.]microsoft-security-alert[.]xyz` | Explicit subdomain routing the phishing email flow. | Add to Secure Email Gateway (SEG) domain blocklist. |
| **Phishing URL** | `hxxp://login[.]microsoftonline[.]com[.]microsoft-security-alert[.]xyz/verify` | The credential harvesting landing page link embedded in the body. | Block at corporate web proxy/web filters. |

---

## 2. Behavioral & Email IOCs

| Indicator Type | Threat Value | Analyst Threat Notes |
| :--- | :--- | :--- |
| **Spoofed Display Name** | `Microsoft Account Team` | Used to masquerade as an internal/trusted system administrator. |
| **Spoofed Domain** | `security@microsoft.com` | Fake sender address used to exploit missing protocol enforcement. |
| **Reply-To Path** | `support@microsoft-security-alert.xyz` | Attacker-controlled inbox meant to hijack manual user responses. |
| **Subject Keyword** | `Urgent: Your account will be suspended` | Social engineering hook relying on panic and psychological fear. |

---

## 3. SIEM Detection & Threat Hunting Queries

To verify if this attack targeted other mailboxes or if any endpoint successfully established a connection with the malicious server, run the following advanced search queries across the SIEM platform:

### A. Email Gateway Hunt (Microsoft Defender / SEG Logs)
```kql
EmailEvents
| where SenderMailFromAddress =~ "security@microsoft.com" or SenderIPv4 == "198.51.100.12"
| project Timestamp, NetworkMessageId, SenderMailFromAddress, RecipientEmailAddress, Subject, DeliveryAction
```

### B. Network Traffic Hunt (Firewall / Web Proxy Logs)
```kql
DeviceNetworkEvents
| where RemoteUrl contains "microsoft-security-alert.xyz" or RemoteIP == "198.51.100.12"
| project Timestamp, DeviceName, InitiatingProcessAccountName, RemoteUrl, RemoteIP, LocalIP
```




