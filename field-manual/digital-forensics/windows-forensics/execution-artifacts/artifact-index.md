---
layout:
  width: wide
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

# Artifact Index

<table><thead><tr><th width="182.33331298828125">Artifact</th><th>Location/Registry Key</th><th>Data Stored</th></tr></thead><tbody><tr><td>Prefetch Files</td><td>C:\Windows\Prefetch</td><td>Metadata about executed applications (file paths, timestamps, execution count)</td></tr><tr><td>Shimcache</td><td>Registry: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache</td><td>Program execution details (file paths, timestamps, flags)</td></tr><tr><td>Amcache</td><td>C:\Windows\AppCompat\Programs\Amcache.hve (Binary Registry Hive)</td><td>Application details (file paths, sizes, digital signatures, timestamps)</td></tr><tr><td>UserAssist</td><td>Registry: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist</td><td>Executed program details (application names, execution counts, timestamps)</td></tr><tr><td>RunMRU Lists</td><td>Registry: HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU</td><td>Recently executed programs and their command lines</td></tr><tr><td>Jump Lists</td><td>User-specific folders (e.g., %AppData%\Microsoft\Windows\Recent)</td><td>Recently accessed files, folders, and tasks associated with applications</td></tr><tr><td>Shortcut (LNK) Files</td><td>Various locations (e.g., Desktop, Start Menu)</td><td>Target executable, file paths, timestamps, user interactions</td></tr><tr><td>Recent Items</td><td>User-specific folders (e.g., %AppData%\Microsoft\Windows\Recent)</td><td>Recently accessed files</td></tr><tr><td>Windows Event Logs</td><td>C:\Windows\System32\winevt\Logs</td><td>Various event logs containing process creation, termination, and other events</td></tr></tbody></table>
