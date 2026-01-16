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
---

# New Technology File System (NTFS)

## The Master File Table (MFT) Structure

The MFT is the heart of NTFS. It is a structured database that contains at least one entry for every file and directory on the volume.

### MFT Records

* Size: Each MFT record is typically 1024 bytes (1KB).
* Header: Contains the "FILE" signature, sequence numbers, and offsets to the first attribute.
* Resident vs. Non-Resident:
  * Resident: If a file is small enough, the data is stored directly within the MFT record.
  * Non-Resident: For larger files, the MFT record contains "Data Runs" (pointers) to clusters on the disk where the actual data resides.

### Critical Metadata Files

NTFS uses "Metafiles" (starting with `$`) to manage the file system:

* $MFT: The MFT itself.
* $MFTMirr: A partial backup of the MFT (first 4 records).
* $Bitmap: Tracks which clusters are in use vs. free.
* $LogFile: The transaction log used for system recovery.

***

## $LogFile Analysis

The `$LogFile` is a circular buffer used by NTFS to ensure file system metadata integrity. If the system crashes, NTFS uses this log to "redo" or "undo" operations to prevent disk corruption.

* Operation: When a file is created or renamed, the change is first written to the `$LogFile`.
* Forensic Value: Even if a file is deleted and its MFT entry is overwritten, traces of its existence (and the original timestamps) may remain in the `$LogFile` for a short period.

> Tools like _Lumasoft_ or _ANSSI-FR's NTFS Log Tracker_ can parse these logs to find "Redo" and "Undo" operations, revealing file movements that happened hours before an investigation began.

***

## MFT Attribute Types: $SI vs. $FN

Every MFT record is composed of attributes. For time-based forensics, the two most important are $STANDARD\_INFORMATION ($SI) and $FILE\_NAME ($FN).

<table data-header-hidden><thead><tr><th>Attribute</th><th width="100">Type ID</th><th>Content</th><th>Access Level</th></tr></thead><tbody><tr><td>$STANDARD_INFORMATION ($SI)</td><td>0x10</td><td>MACB timestamps, file permissions, owner ID.</td><td>Updated by general system API calls.</td></tr><tr><td>$FILE_NAME ($FN)</td><td>0x30</td><td>File name, parent directory, size, and MACB timestamps.</td><td>Updated only by the NTFS Kernel (rarely by users).</td></tr></tbody></table>

> Note: "MACB" stands for Modification, Access, Creation, and MFT Entry Birth/Change.

***

## Timestomping and Forensic Detection

Timestomping is an anti-forensic technique where an attacker manually changes a file's timestamps (usually the Creation date) to make a malicious file look like it belongs to the original Windows installation.

### How Timestomping Affects Attributes

When an attacker uses a tool to change a file's time, they almost always target the $STANDARD\_INFORMATION ($SI) attribute because it is easily accessible via the Windows API.

However, the $FILE\_NAME ($FN) attribute is much harder to modify because the OS only updates it during specific events (like moving or renaming a file).

### Detection Table: The "Time Mismatch"

Forensic analysts look for a discrepancy between these two attributes to identify manipulation:

| Scenario           | $SI Timestamps | $FN Timestamps | Conclusion             |
| ------------------ | -------------- | -------------- | ---------------------- |
| Normal File        | Matches $FN    | Matches $SI    | Legitimate file.       |
| Timestomped File   | 2010 (Fake)    | 2024 (Actual)  | Manipulation Detected. |
| File Moved/Renamed | Original       | Updated        | Normal OS behavior.    |

### Detecting "Zero-Millisecond" Precision

Another red flag is the precision of the timestamp. While NTFS tracks time in 100-nanosecond intervals, many timestomping tools only set time to the second, resulting in a timestamp like `2023-01-01 12:00:00.0000000`. Genuine Windows timestamps rarely end in perfect zeros across the entire fractional section.
