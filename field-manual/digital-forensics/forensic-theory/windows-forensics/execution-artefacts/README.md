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

# Execution Artefacts

Execution artefacts are system-generated traces that conclusively prove a specific binary or executable ran on a system. By cross-referencing these artefacts, we can answer the four core forensic questions: What ran, when did it run, where did it execute from, and who ran it?

<table><thead><tr><th width="182.33331298828125">Artifact</th><th width="327">Location/Registry Key</th><th width="295">Data Stored</th><th width="151">Retained on Reboot?</th></tr></thead><tbody><tr><td><a data-mention href="prefetch-files.md">prefetch-files.md</a></td><td>C:\Windows\Prefetch</td><td>Metadata about executed applications (file paths, timestamps, execution count)</td><td>Yes</td></tr><tr><td><a data-mention href="shimcache.md">shimcache.md</a></td><td>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache</td><td>Program execution details (file paths, timestamps, flags)</td><td>Yes (written on shutdown)</td></tr><tr><td><a data-mention href="amcache.md">amcache.md</a></td><td>C:\Windows\AppCompat\Programs\Amcache.hve (Binary Registry Hive)</td><td>Application details (file paths, sizes, digital signatures, timestamps)</td><td>Yes</td></tr><tr><td><a data-mention href="userassist.md">userassist.md</a></td><td>HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist</td><td>Executed program details (application names, execution counts, timestamps)</td><td>Yes</td></tr><tr><td><a data-mention href="background-activity-moderator-bam.md">background-activity-moderator-bam.md</a></td><td>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\State\UserSettings<code>{SID}</code><br><br>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\UserSettings<code>{SID}</code></td><td>User SID, full executable path, recent execution time</td><td>Volatile (7-day decay)</td></tr><tr><td><a data-mention href="desktop-activity-moderator-dam.md">desktop-activity-moderator-dam.md</a></td><td><p></p><p>HKLM\SYSTEM\CurrentControlSet\Services\dam\UserSettings\<code>{USER_SID}</code></p><p></p><p>HKLM\SYSTEM\CurrentControlSet\Services\dam\state\UserSettings\<code>{USER_SID}</code></p></td><td>User SID, full executable path, recent execution time</td><td>Volatile (7-day decay)</td></tr><tr><td><a data-mention href="runmru-lists.md">runmru-lists.md</a></td><td>HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU</td><td>Recently executed programs and their command lines</td><td>Yes</td></tr><tr><td><a data-mention href="jump-lists.md">jump-lists.md</a></td><td>User-specific folders (e.g., %AppData%\Microsoft\Windows\Recent)</td><td>Recently accessed files, folders, and tasks associated with applications</td><td>Yes</td></tr><tr><td><a data-mention href="shortcut-lnk-files.md">shortcut-lnk-files.md</a></td><td>Various locations (e.g., Desktop, Start Menu)</td><td>Target executable, file paths, timestamps, user interactions</td><td>Yes</td></tr><tr><td><a data-mention href="recent-items.md">recent-items.md</a></td><td>User-specific folders (e.g., %AppData%\Microsoft\Windows\Recent)</td><td>Recently accessed files</td><td>Yes</td></tr><tr><td><a data-mention href="windows-event-logs.md">windows-event-logs.md</a></td><td>C:\Windows\System32\winevt\Logs</td><td>Various event logs containing process creation, termination, and other events</td><td>Yes</td></tr></tbody></table>
