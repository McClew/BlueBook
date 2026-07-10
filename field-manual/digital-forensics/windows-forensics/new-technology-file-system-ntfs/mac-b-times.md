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

All these timestamps reside in the [master-file-table-mft.md](master-file-table-mft.md "mention") file, located at the root of the system drive. These timestamps are housed within the `$MFT` across two distinct attributes:

* `$STANDARD_INFORMATION`
* `$FILE_NAME`

The timestamps visible in the Windows file explorer are derived from the `$STANDARD_INFORMATION` attribute.
