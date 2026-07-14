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

# Account Usage & Authentication Artefacts

Authentication artefacts track the lifecycle of a user session - from the initial connection request and credential validation to session disconnection. In Windows, these events are split across active memory structures, registry databases, and high-fidelity event log channels.

<table data-search="true"><thead><tr><th>Artefact Name</th><th>Location</th><th>Forensic Focus</th><th>Retained on Reboot?</th></tr></thead><tbody><tr><td><a data-mention href="security-event-id-4624.md">security-event-id-4624.md</a></td><td><code>Security.evtx</code> Log</td><td>Successful logons, logon types, source IPs</td><td>Yes</td></tr><tr><td><a data-mention href="security-event-id-4625.md">security-event-id-4625.md</a></td><td><code>Security.evtx</code> Log</td><td>Failed logons, structural failure reasons, targeted accounts</td><td>Yes</td></tr><tr><td><a data-mention href="the-sam-hive.md">the-sam-hive.md</a></td><td><code>C:\Windows\System32\config\SAM</code></td><td>Local user accounts, RIDs, login counts, password age</td><td>Yes</td></tr><tr><td>RDP Operational Logs</td><td>RemoteConnectionManager &#x26; LocalSessionManager <code>.evtx</code></td><td>RDP connection handshakes, source hostnames, session states</td><td>Yes</td></tr><tr><td>Event IDs 4720 &#x26; 4722</td><td><code>Security.evtx</code> Log</td><td>Rogue user account creation and status modification</td><td>Yes</td></tr></tbody></table>
