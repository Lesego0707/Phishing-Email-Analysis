# Email Header Analysis

## 1. Case Information

| Field | Details |
|---|---|
| Case ID | PHISH-001 |
| Analysis Type | Email Header Investigation |
| Evidence Type | Synthetic training data |
| Status | Educational exercise |

## 2. Investigation Objective

The objective is to understand how email headers can help an analyst investigate sender identity, message routing, and email authentication.

Email headers can contain information such as the sender, recipient, timestamps, routing servers, return path, and authentication results.

## 3. Sample Header Evidence

The following is a fictional example for learning purposes. It is not extracted from a real email.

```text
From: Microsoft Account Team <security@example.invalid>
Reply-To: support@example.invalid
Return-Path: <bounce@example.invalid>
Subject: Urgent: Your account will be suspended
Authentication-Results: mx.training.invalid;
    spf=fail;
    dkim=none;
    dmarc=fail
```

**Important:** The authentication results above are invented training values. They do not establish that the original simulated email passed through a mail server or that any real domain failed authentication.

## 4. Header Field Analysis

### From

Identifies the sender address displayed in the email.

**Investigation question:** Does the sender's claimed identity match the actual domain and the context of the message?

The display name alone is not sufficient to authenticate a sender.

### Reply-To

Specifies where replies may be directed.

**Investigation question:** Is the reply destination expected and consistent with the claimed sender?

A different Reply-To address warrants examination but is not, by itself, proof of phishing.

### Return-Path

Typically identifies the address used for handling delivery failures, based on the message's envelope sender.

**Investigation question:** Is this address consistent with the expected sending infrastructure?

Differences between From and Return-Path can occur in legitimate email systems.

### Authentication-Results

Records authentication checks performed by a receiving mail system.

The fictional example shows SPF failure, no DKIM result, and DMARC failure. In a genuine investigation, these results would need to be examined alongside the receiving server, domain alignment, message routing, and other evidence.

## 5. SPF, DKIM, and DMARC

| Mechanism | What It Checks | What to Investigate |
|---|---|---|
| SPF | Whether the sending IP is authorized by the relevant domain's SPF policy | SPF result and the domain evaluated |
| DKIM | Whether a cryptographic signature validates for the signed message and domain | Signature validation and signing domain |
| DMARC | Whether SPF and/or DKIM pass with the required alignment to the visible From domain | DMARC result and alignment details |

A failed authentication check does not automatically mean an email is malicious. Forwarding, configuration errors, and legitimate third-party services can affect results. Conversely, passing authentication does not guarantee that an email is safe.

## 6. Preliminary Assessment

The fictional header includes authentication failures that, in a real investigation, would justify further examination.

However, because these results are synthetic, no conclusion about real sender infrastructure or malicious activity can be drawn from them.

**Classification:** Training exercise — no real email authentication result verified.

## 7. Further Investigation Steps

For a genuine suspicious email obtained through an authorized process:

1. Preserve the original message and full headers.
2. Identify the receiving mail server and determine which system generated the authentication results.
3. Examine the actual sending IP and relevant domains.
4. Review SPF, DKIM, and DMARC results and alignment.
5. Correlate header findings with message content, URLs, attachments, and other available evidence.
6. Document confirmed findings and remaining uncertainties in the incident report.

## 8. Lessons Learned

Email headers provide technical context that is not always visible in the email body. Understanding sender identity, routing, and authentication helps analysts investigate suspicious messages more systematically.

Authentication results are evidence to interpret, not a standalone verdict. Sound SOC analysis requires correlation, context, and clear documentation of evidence limitations.
