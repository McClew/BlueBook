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

# Windows Anti-Forensics

Anti-forensics refers to any deliberate action taken by an adversary to manipulate, corrupt, delete, or obscure forensic evidence. In a Windows environment, this typically targets file system metadata, system event logs, volume backups, and registry traces.

By understanding _how_ attackers attempt to blind us, we can turn their cover-up attempts into some of our strongest indicators of compromise (IoCs).

<table data-search="true"><thead><tr><th width="176">Technique</th><th width="213">Target</th><th width="242">Indicator</th><th width="114">Retained on Reboot?</th></tr></thead><tbody><tr><td><a data-mention href="timestomping.md">timestomping.md</a></td><td>NTFS File Metadata</td><td><code>$STANDARD_INFORMATION</code> vs <code>$FILE_NAME</code> Mismatch</td><td>Yes</td></tr><tr><td><a data-mention href="log-clearance.md">log-clearance.md</a></td><td>Event Log Service (<code>.evtx</code>)</td><td>Security Event ID 1102 / System Event ID 104</td><td>Yes</td></tr><tr><td><a data-mention href="volume-shadow-copy-vss-deletion.md">volume-shadow-copy-vss-deletion.md</a></td><td>Windows Backup States (VSS)</td><td>Sudden loss of system restore points / VSS logs</td><td>Yes</td></tr><tr><td></td><td>Disk Space &#x26; Master File Table</td><td>Orphaned directory entries / <code>$MFT</code> record reuse</td><td>Yes</td></tr><tr><td>Event Log Suspension</td><td>Active Memory (Threads)</td><td>Gaps in continuous event sequence IDs</td><td>No (Resumes post-boot)</td></tr></tbody></table>
