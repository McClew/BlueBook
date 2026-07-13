---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Investigating Exchange Forwarding Rules

Threat actors frequently create inbox rules to forward emails to external addresses. This establishes persistence and automates data exfiltration. Analysing these events via Microsoft Purviews' Unified Audit Log (UAL) is a primary step in business email compromise (BEC) investigations.

***

## Target Operations

When querying Purview, filter for the following Exchange cmdlets:

* `New-InboxRule`
* `Set-InboxRule`
* `Enable-InboxRule`

***

## Analysing Purview JSON Output

The raw JSON payload contains the specific configuration of the rule. The most critical data resides within the `Parameters` array.

Crucial Fields to Inspect:

* `UserId`: The compromised account executing the change.
* `ClientIPAddress`: The origin IP address. Pivot on this to find associated malicious logins.
* `Parameters`: Inspect the array for the following keys:
  * `ForwardTo`
  * `ForwardAsAttachmentTo`
  * `RedirectTo`
  * `MoveToFolder` (often used to hide emails in RSS Subscriptions or Archive)
  * `DeleteMessage` (used to destroy evidence of the forward)

### Example JSON Snippet

```json
{
  "CreationTime": "2026-07-09T10:15:30",
  "Operation": "New-InboxRule",
  "Workload": "Exchange",
  "UserId": "victim@domain.co.uk",
  "ClientIPAddress": "203.0.113.50",
  "Parameters": [
    {
      "Name": "Name",
      "Value": "..." 
    },
    {
      "Name": "ForwardTo",
      "Value": "exfiltration@external-domain.com"
    },
    {
      "Name": "StopProcessingRules",
      "Value": "True"
    },
    {
      "Name": "DeleteMessage",
      "Value": "True"
    }
  ]
}
```

### Handling Real-World Purview Output

When exporting logs via the Purview GUI or PowerShell, the exact rule configurations are often trapped inside escaped strings rather than formatted JSON objects.

{% code title="Realistic Output Snippet (Stringified)" overflow="wrap" %}
```json
"Parameters": "[{\"Name\":\"RuleName\",\"Value\":\"Spam Filter\"},{\"Name\":\"ForwardTo\",\"Value\":\"exfiltration@external-domain.com\"},{\"Name\":\"DeleteMessage\",\"Value\":\"True\"}]"
```
{% endcode %}

To triage effectively, analysts must reconstruct this stringified data into a readable format.

* **Via PowerShell:** If pulling logs via `Search-UnifiedAuditLog`, expand the `AuditData` property and convert it dynamically.

{% code overflow="wrap" %}
```powershell
$AuditLogs = Search-UnifiedAuditLog -RecordType ExchangeAdmin -Operations "New-InboxRule" -StartDate (Get-Date).AddDays(-7) -EndDate (Get-Date)

# Parse the stringified AuditData into readable objects
$ParsedLogs = $AuditLogs | ForEach-Object { $_.AuditData | ConvertFrom-Json }

# Extract the nested parameters
$ParsedLogs | Select-Object UserId, CreationTime, Parameters
```
{% endcode %}

* **Via CyberChef:** If you have exported a CSV directly from the Purview portal, copy the raw, messy `AuditData` or `Parameters` cell into CyberChef. Apply the Unescape String recipe followed by the JSON Beautify recipe to reveal the clean structure.
* **Via SIEM / Log Aggregators:** Ensure your ingestion pipeline (e.g., Splunk, Sentinel) is configured to automatically parse and extract JSON fields from the `AuditData` string upon ingestion. If it relies on raw text searches, querying for exact matches like `"Name":"ForwardTo"` will be required.

***

## Forensic Triage Steps

1. Identify the Destination: Extract the `ForwardTo` or `RedirectTo` value. Verify if the external domain is legitimate or unauthorised.
2. Evaluate the Rule Name: Attackers often use deceptive or blank names (e.g., ".", " ", "Sync", "Spam Filter") to avoid user detection.
3. Check for Evasion: A rule that forwards an email and simultaneously sets `DeleteMessage` to `True` is highly indicative of malicious intent.
4. Remediation: If confirmed malicious, immediately disable the rule via Exchange PowerShell (`Disable-InboxRule`) or the Exchange Admin Centre, reset the user's credentials, and revoke existing session tokens.
