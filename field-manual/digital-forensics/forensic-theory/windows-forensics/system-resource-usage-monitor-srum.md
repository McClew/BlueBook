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

# System Resource Usage Monitor (SRUM)

`SRUM` (System Resource Usage Monitor) is a feature introduced in Windows 8 and subsequent versions. SRUM meticulously tracks resource utilisation and application usage patterns.

The data is housed in a database file named `sru.db` found in the `C:\Windows\System32\sru` directory. This SQLite formatted database allows for structured data storage and efficient data retrieval.

SRUM's records, organised by time intervals, can help reconstruct application and resource usage over specific durations.

Key facets of SRUM forensics encompass:

* `Application Profiling`: SRUM can provide a comprehensive view of the applications and processes that have been executed on a Windows system. It records details such as executable names, file paths, timestamps, and resource usage metrics. This information is crucial for understanding the software landscape on a system, identifying potentially malicious or unauthorised applications, and reconstructing user activities.
* `Resource Consumption`: SRUM captures data on CPU time, network usage, and memory consumption for each application and process. This data is invaluable for investigating resource-intensive activities, identifying unusual patterns of resource consumption, and detecting potential performance issues caused by specific applications.
* `Timeline Reconstruction`: By analysing SRUM data, digital forensics experts can create timelines of application and process execution, resource usage, and system activities. This timeline reconstruction is instrumental in understanding the sequence of events, identifying suspicious behaviours, and establishing a clear picture of user interactions and actions.
* `User and System Context`: SRUM data includes user identifiers, which helps in attributing activities to specific users. This can aid in user behaviour analysis and determining whether certain actions were performed by legitimate users or potential threat actors.
* `Malware Analysis & Detection`: SRUM data can be used to identify unusual or unauthorised applications that may be indicative of malware or malicious activities. Sudden spikes in resource usage, abnormal application patterns, or unauthorized software installations can all be detected through SRUM analysis.
* `Incident Response`: During incident response, SRUM can provide rapid insights into recent application and process activities, enabling analysts to quickly identify potential threats and respond effectively.
