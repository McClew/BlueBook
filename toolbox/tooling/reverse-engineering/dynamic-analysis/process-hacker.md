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
---

# Process Hacker

{% hint style="info" %}
#### Download & Install

\-
{% endhint %}

***

Process Hacker makes it easy to examine processes by listing processes in a hierarchical view. When the malware creates a new process, you can see the newly created process under its parent process.

Malware can inject itself into different processes, perform activities for its own purposes with living of the land binaries, or make legitimate applications run their own applications. For these reasons, the activities of all processes belonging to the malware and used by the malware should be analysed.

For instance, let’s say the malware injects itself into the `notepad.exe` process after it runs. In this case, we need to examine all of the activities that notepad.exe has created since the moment it was injected.

