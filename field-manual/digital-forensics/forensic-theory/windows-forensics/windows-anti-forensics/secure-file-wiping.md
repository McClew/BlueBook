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

# Secure File Wiping

Rather than using standard deletion, which leaves file data intact in unallocated space, adversaries may use file-shredding utilities (like Sysinternals `SDelete`) to overwrite data with random characters or zeroes.
