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
---

# Hunting for Suspicious M365 Exchange Rules

Identifying unauthorised inbox rules used for data exfiltration, business email compromise (BEC), or evidence tampering.

***

## Indicators of Compromise

When reviewing the output, hunt for these specific red flags:

<table><thead><tr><th width="118">Attribute</th><th>Suspicious Pattern</th><th>Intent</th></tr></thead><tbody><tr><td>Name</td><td>".", "...", or blank names</td><td>Hiding the rule from the user UI.</td></tr><tr><td>Action</td><td><code>MoveToFolder: 'Deleted Items'</code></td><td>Deleting incoming alerts (e.g., "Password Changed").</td></tr><tr><td>Action</td><td><code>MarkAsRead</code></td><td>Preventing the user from noticing new "Unread" mail.</td></tr><tr><td>Destination</td><td>External/Personal domains (Gmail, ProtonMail)</td><td>Data exfiltration.</td></tr><tr><td>Keywords</td><td>"Invoice", "Payment", "Wire", "Urgent"</td><td>Intercepting financial transactions.</td></tr></tbody></table>

***

## Forwarding Rule Discovery

Standard Outlook interfaces (Web and Desktop) often fail to show Hidden Rules. These are frequently used by attackers to "black hole" security alerts or IT notifications.

A collection of snippets can be found at [get-inboxrule.md](../../../toolbox/snippets/powershell/get-inboxrule.md "mention").

{% code title="Connect to Exchange Online first" overflow="wrap" lineNumbers="true" %}
```powershell
Connect-ExchangeOnline
```
{% endcode %}

{% code title="Pull a high-fidelity list of all rules for a target mailbox" overflow="wrap" lineNumbers="true" %}
```powershell
$User = "user@domain.com"

Get-InboxRule -Mailbox $User -IncludeHidden | 
Select-Object Name, Priority, Enabled, MoveToFolder, ForwardTo, RedirectTo, DeleteMessage, MarkAsRead, Description | 
Format-List
```
{% endcode %}

{% hint style="info" %}
#### Why use `Format-List` here?

Unlike the summary view in our previous KB, `Format-List` ensures the Description property isn't truncated. The Description often contains the exact logic (e.g., _"If the message contains 'Invoice', move to Deleted Items"_), which is critical for identifying intent.
{% endhint %}

***

## Bulk Hunting

Instead of checking one mailbox, use the below script to find forwarding rules across the entire tenant. This helps identify if a threat actor has compromised multiple accounts.

{% code title="Connect to Exchange Online first" overflow="wrap" lineNumbers="true" %}
```powershell
Connect-ExchangeOnline
```
{% endcode %}

<pre class="language-powershell" data-title="Find every inbox rule in the tenant that forwards or redirects mail" data-overflow="wrap" data-line-numbers><code class="lang-powershell">$AllMailboxes = Get-Mailbox -ResultSize Unlimited
foreach ($Mailbox in $AllMailboxes) {
    Get-InboxRule -Mailbox $Mailbox.DistinguishedName -IncludeHidden | 
<strong>    Where-Object { $_.ForwardTo -ne $null -or $_.RedirectTo -ne $null -or $_.ForwardAsAttachmentTo -ne $null } |
</strong>    Select-Object MailboxOwnerID, Name, Enabled, RedirectTo, ForwardTo, Description
}
</code></pre>
