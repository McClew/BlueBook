# Get-InboxRule

Connect to Exchange Online before running query commands.

{% code lineNumbers="true" %}
```powershell
Connect-ExchangeOnline
```
{% endcode %}

Basic command:

{% code lineNumbers="true" %}
```powershell
Get-InboxRule -Mailbox user@domain.com
```
{% endcode %}

Get information on hidden rules:

{% code overflow="wrap" lineNumbers="true" %}
```powershell
Get-InboxRule -Mailbox accounts@domain.co.uk -IncludeHidden | Select-Object Name, Enabled, RedirectTo, ForwardTo, ForwardAsAttachmentTo
```
{% endcode %}

Get detailed information on forwarding rules:

{% code overflow="wrap" lineNumbers="true" %}
```powershell
Get-InboxRule -Mailbox accounts@uknational.co.uk -IncludeHidden | Select-Object Name, Provider, Enabled, Priority, LastModifiedTime, MoveToFolder, Action, RedirectTo, ForwardTo, Description | Format-List
```
{% endcode %}
