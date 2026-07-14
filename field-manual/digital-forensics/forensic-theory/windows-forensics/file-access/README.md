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

# File Access Artefacts

File and folder access artefacts track a user's interaction with the system's file structures. Windows maintains these traces to provide a seamless user experience - remembering window sizes, icon positions, and recently used files. For an investigator, these system conveniences serve as a reliable audit trail of user activity.

<table data-search="true"><thead><tr><th>Artefact Name</th><th>Location</th><th>Forensic Focus</th><th>Retained on Reboot?</th></tr></thead><tbody><tr><td><a data-mention href="shellbags.md">shellbags.md</a></td><td><code>UsrClass.dat</code> &#x26; <code>NTUSER.DAT</code></td><td>Folder navigation, directory structures, views</td><td>Yes</td></tr><tr><td><a data-mention href="recentdocs.md">recentdocs.md</a></td><td><code>NTUSER.DAT</code> Registry Hive</td><td>Recently opened files (by extension structure)</td><td>Yes</td></tr><tr><td><a data-mention href="opensavemru.md">opensavemru.md</a></td><td><code>NTUSER.DAT</code> Registry Hive</td><td>Files tracked via Open/Save dialogue windows</td><td>Yes</td></tr><tr><td><a data-mention href="lnk-files-and-recent-items.md">lnk-files-and-recent-items.md</a></td><td>AppData File System Directory</td><td>Shortcuts to recently opened files/folders</td><td>Yes</td></tr><tr><td><a data-mention href="jump-lists.md">jump-lists.md</a></td><td>AppData File System Directory</td><td>Application-specific document interaction history</td><td>Yes</td></tr></tbody></table>
