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

# RDP Operational Logs

While the Security log tracks the core authentication, Windows maintains dedicated operational logs to track the network transport and session negotiation of Remote Desktop connections. This corroborates network source metadata and session reconnection events.

**Paths:**

* &#x20;`...\Winevt\Logs\Microsoft-Windows-TerminalServices-RemoteConnectionManager%4Operational.evtx`
* `...\Winevt\Logs\Microsoft-Windows-TerminalServices-LocalSessionManager%4Operational.evtx`

When an attacker connects via RDP, `RemoteConnectionManager Event ID 1149` captures the successful network authentication handshake _before_ the user's desktop environment is built. This event records the Source IP and the Source Workstation Name provided by the connecting client.&#x20;

Crucially, if a threat actor disconnects without logging off and later reconnects to hijack their active session, `LocalSessionManager Event ID 25` will record the reconnection event, letting you accurately track the lifespan of their network session.
