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

# Event IDs 4720 & 4722

These events monitor the administrative modification of user security contexts across the local system. These logs track the creation, enablement, and configuration changes of local user profiles.

**Path:** `C:\Windows\System32\Winevt\Logs\Security.evtx`

> #### #4720
>
> **A user account was created**
>
> Attributes show some of the properties that were set at the time the account was created. Notice account is initially disabled.
>
> This event is logged both for local SAM accounts and domain accounts.
>
> You will see a series of other User Account Management events after this event as the remaining properties are punched down, password set and account finally enabled.

> #### #4722
>
> **A user account was enabled**
>
> The user identified by Subject: enabled the user identified by Target Account.&#x20;
>
> This event is logged both for local SAM accounts and domain accounts.
>
> This event is always logged after event [4720](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4720) - user account creation.
>
> You will also see event ID [4738](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4738) informing you of the same information.

Threat actors frequently establish backdoors by creating a new local user account and adding it to the local Administrators group. `Event ID 4720` triggers the moment a new account is provisioned, while `Event ID 4722` captures when that account is enabled.

Both logs explicitly record the Subject ID, giving us a direct link back to the compromised administrator account the attacker was using at the time.
