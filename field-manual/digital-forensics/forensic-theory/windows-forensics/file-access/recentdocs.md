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

# RecentDocs

The `RecentDocs` registry key tracks the most recently accessed files, organised globally and broken down systematically by file extension type. This provides a historical, chronological list of files opened by the user account context.

**Path:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`

***

## Extension Subkeys

Entries inside the `RecentDocs` key are ordered using an internal binary MRUListEx tracking string. When parsed, this registry key reveals a dual-layered mapping system: it contains the global execution history order alongside distinct subkeys for individual file extensions (e.g., `.docx`, `.pdf`, `.zip`).

This allows us to filter your analysis specifically to high-risk file types when searching for data staging tools or compressed archives.
