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

# MAC(b) Times

The term `MAC(b) times` denotes a series of timestamps linked to files or objects. These timestamps are pivotal as they shed light on the chronology of events or actions on a file system.

The acronym `MAC(b)` is an abbreviation for `Modified, Accessed, Changed, and (b) Birth` times. The inclusion of `b` signifies the `Birth timestamp`, which isn't universally present across all file systems or easily accessible via standard Windows API functions.



* `Modified Time (M)`: This timestamp captures the last instance when the content within the file underwent modifications. Any alterations to the file's data, such as content edits, trigger an update to this timestamp.
* `Accessed Time (A)`: This timestamp reflects the last occasion when the file was accessed or read, updating whenever the file is opened or otherwise engaged.
* `Changed [Change in MFT Record ] (C)`: This timestamp signifies changes to the MFT record. It captures the moment when the file was initially created. However, it's worth noting that certain file systems, like NTFS, might update this timestamp if the file undergoes movement or copying.
* `Birth Time (b)`: Often referred to as the Birth or Born timestamp, this represents the precise moment when the file or object was instantiated on the file system. Its significance in forensic investigations cannot be overstated, especially when determining a file's original creation time.

***

## Timestamp Rules Map

The table below delineates the general rules governing how various file operations influence the timestamps within the Windows NTFS (New Technology File System).

| Operation   | Modified       | Accessed | Birth (Created) |
| ----------- | -------------- | -------- | --------------- |
| File Create | Yes            | Yes      | Yes             |
| File Modify | Yes            | No       | No              |
| File Copy   | No (Inherited) | Yes      | Yes             |
| File Access | No             | No\*     | No              |

1. **File Create**:
   * `Modified Timestamp (M)`: The Modified timestamp is updated to reflect the time of file creation.
   * `Accessed Timestamp (A)`: The Accessed timestamp is updated to reflect that the file was accessed at the time of creation.
   * `Birth (Created) Timestamp (b)`: The Birth timestamp is set to the time of file creation.
2. **File Modify**:
   * `Modified Timestamp (M)`: The Modified timestamp is updated to reflect the time when the file's content or attributes were last modified.
   * `Accessed Timestamp (A)`: The Accessed timestamp is not updated when the file is modified.
   * `Birth (Created) Timestamp (b)`: The Birth timestamp is not updated when the file is modified.
3. **File Copy**:
   * `Modified Timestamp (M)`: The Modified timestamp is typically not updated when a file is copied. It usually inherits the timestamp from the source file.
   * `Accessed Timestamp (A)`: The Accessed timestamp is updated to reflect that the file was accessed at the time of copying.
   * `Birth (Created) Timestamp (b)`: The Birth timestamp is updated to the time of copying, indicating when the copy was created.
4. **File Access**:
   * `Modified Timestamp (M)`: The Modified timestamp is not updated when the file is accessed.
   * `Accessed Timestamp (A)`: The Accessed timestamp is updated to reflect the time of access.
   * `Birth (Created) Timestamp (b)`: The Birth timestamp is not updated when the file is accessed.

All these timestamps reside in the [.](./ "mention") file, located at the root of the system drive. These timestamps are housed within the `$MFT` across two distinct attributes:

* `$STANDARD_INFORMATION`
* `$FILE_NAME`

The timestamps visible in the Windows file explorer are derived from the `$STANDARD_INFORMATION` attribute.

***

## Timestomping Investigation

Identifying instances of timestamp manipulation, commonly termed as timestomping ([T1070.006](https://attack.mitre.org/techniques/T1070/006/)), presents a formidable challenge in digital forensics. Timestomping entails the alteration of file timestamps to obfuscate the sequence of file activities. This tactic is frequently employed by various tools, as illustrated in the MITRE ATT\&CK's timestomp technique.

![Screenshot of MITRE ATT\&CK webpage showing the Timestomp technique. Highlights include Cobalt Strike and Empire tools, which can modify file timestamps to help files blend in. The left menu lists various indicator removal techniques.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/237/win_dfir_mft_time3.png)

When adversaries manipulate file creation times or deploy tools for such purposes, the timestamp displayed in the file explorer undergoes modification.

For instance, if we load `C:\Users\johndoe\Desktop\forensic_data\kape_output\D\$MFT` into `MFT Explorer` we will notice that the creation time of the file `ChangedFileTime.txt` has been tampered with, displaying `03-01-2022` in the file explorer, which deviates from the actual creation time.

![Screenshot of MFT Explorer v2.0.0.0 showing file details in a forensic analysis. The file 'ChangedFileTime.txt' in the Temp directory is highlighted, with timestamps indicating creation on 2022-01-03 and modification on 2023-09-07. The properties pane shows 'Possible Timestamped' checked.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/237/img1.png)

However, given our knowledge that the timestamps in the file explorer originate from the `$STANDARD_INFORMATION` attribute, we can cross-verify this data with the timestamps from the `$FILE_NAME` attribute through `MFTEcmd` as follows.

```powershell
PS C:\Users\johndoe\Desktop\Get-ZimmermanTools\net6> .\MFTECmd.exe -f 'C:\Users\johndoe\Desktop\forensic_data\kape_output\D\$MFT' --de 0x16169
MFTECmd version 1.2.2.1

Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/MFTECmd

Command line: -f C:\Users\johndoe\Desktop\forensic_data\kape_output\D\$MFT --de 0x16169

Warning: Administrator privileges not found!

File type: Mft

Processed C:\Users\johndoe\Desktop\forensic_data\kape_output\D\$MFT in 3.4924 seconds

C:\Users\johndoe\Desktop\forensic_data\kape_output\D\$MFT: FILE records found: 93,615 (Free records: 287) File size: 91.8MB


Dumping details for file record with key 00016169-00000004

Entry-seq #: 0x16169-0x4, Offset: 0x585A400, Flags: InUse, Log seq #: 0xCC5FB25, Base Record entry-seq: 0x0-0x0
Reference count: 0x2, FixUp Data Expected: 04-00, FixUp Data Actual: 00-00 | 00-00 (FixUp OK: True)

**** STANDARD INFO ****
  Attribute #: 0x0, Size: 0x60, Content size: 0x48, Name size: 0x0, ContentOffset 0x18. Resident: True
  Flags: Archive, Max Version: 0x0, Flags 2: None, Class Id: 0x0, Owner Id: 0x0, Security Id: 0x557, Quota charged: 0x0, Update sequence #: 0x8B71F8

  Created On:         2022-01-03 16:54:25.2726453
  Modified On:        2023-09-07 08:30:12.4258743
  Record Modified On: 2023-09-07 08:30:12.4565632
  Last Accessed On:   2023-09-07 08:30:12.4258743

**** FILE NAME ****
  Attribute #: 0x3, Size: 0x78, Content size: 0x5A, Name size: 0x0, ContentOffset 0x18. Resident: True

  File name: CHANGE~1.TXT
  Flags: Archive, Name Type: Dos, Reparse Value: 0x0, Physical Size: 0x0, Logical Size: 0x0
  Parent Entry-seq #: 0x16947-0x2

  Created On:         2023-09-07 08:30:12.4258743
  Modified On:        2023-09-07 08:30:12.4258743
  Record Modified On: 2023-09-07 08:30:12.4258743
  Last Accessed On:   2023-09-07 08:30:12.4258743

**** FILE NAME ****
  Attribute #: 0x2, Size: 0x80, Content size: 0x68, Name size: 0x0, ContentOffset 0x18. Resident: True

  File name: ChangedFileTime.txt
  Flags: Archive, Name Type: Windows, Reparse Value: 0x0, Physical Size: 0x0, Logical Size: 0x0
  Parent Entry-seq #: 0x16947-0x2

  Created On:         2023-09-07 08:30:12.4258743
  Modified On:        2023-09-07 08:30:12.4258743
  Record Modified On: 2023-09-07 08:30:12.4258743
  Last Accessed On:   2023-09-07 08:30:12.4258743

**** DATA ****
  Attribute #: 0x1, Size: 0x18, Content size: 0x0, Name size: 0x0, ContentOffset 0x18. Resident: True

  Resident Data

  Data:

    ASCII:
    UNICODE:

```

![Screenshot showing STANDARD INFO with timestamps. 'Created On' is highlighted as 2022-01-03, indicating timestomping in $STANDARD\_INFO.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/237/win_dfir_mft_time5.png)

![File details for 'ChangedFileTime.txt' showing creation date as 2023-09-07, indicating original creation time in $FILE\_NAME.](https://cdn.services-k8s.prod.aws.htb.systems/content/modules/237/win_dfir_mft_time6.png)

In standard Windows file systems like NTFS, regular users typically lack the permissions to directly modify the timestamps of filenames in `$FILE_NAME`. Such modifications are exclusively within the purview of the system kernel.
