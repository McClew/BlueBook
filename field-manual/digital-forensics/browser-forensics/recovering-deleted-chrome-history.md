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

# Recovering Deleted Chrome History

SQLite uses temporary files to manage transactions. When a user deletes their history, the "deleted" data often persists in these auxiliary files until the database is "checkpointed" or optimised.

***

## Analysis Steps

{% stepper %}
{% step %}
#### Check for existence

Always check if `History-wal` exists. If it does, its size will tell you how much uncommitted data is available.
{% endstep %}

{% step %}
#### Use Forensic Tools

Tools like [db-browser-for-sqlite.md](../../../toolbox/tooling/utilities/db-browser-for-sqlite.md "mention") will sufice, but specialised tools like [browsinghistoryview.md](../../../toolbox/tooling/digital-forensics/browsinghistoryview.md "mention") or [magnet-axiom.md](../../../toolbox/tooling/digital-forensics/magnet-axiom.md "mention") are better at automatically parsing the deleted records in SQLite.
{% endstep %}

{% step %}
#### Cross-Reference with NTFS

If we find a deleted download record, check the `$MFT` (Master File Table) or `$UsnJrnl` for a file creation record at that same timestamp to prove the file actually hit the disk.
{% endstep %}
{% endstepper %}

***

## Identifying the Target Files

In the same directory as your `History` file, look for:

* `History-journal`: Created during a rollback state.
* `History-wal`: The Write-Ahead Log. This contains new/modified data that hasn't been fully merged into the main `History` file yet.

***

## Recovery Techniques

### **The Copy Method**

If you find a `History-wal` file, do not delete it. To see the most recent (and potentially deleted) data:

1. Copy both `History` and `History-wal` to our analysis workstation.
2. Keep them in the same folder.
3. Open the `History` file in a SQLite viewer. The viewer will automatically use the `-wal` file to "replay" the most recent transactions, showing you data that hasn't been committed yet.

### **The Grepping Method**

If the database has already been optimised, the records are marked as "free" but the actual text remains in unallocated space until overwritten. You can use `strings` or a hex editor to search the `History` file for keywords:

* `http` or `https` (To find URL remnants)
* `.exe`, `.zip`, `.docm` (To find deleted download references)
* The filename of the known malware.

{% code title="Search the History file for specific file extensions even if deleted from the DB" %}
```powershell
Select-String -Path ".\History" -Pattern "\.zip|\.exe|\.msi" -AllMatches | Select-Object Line
```
{% endcode %}

***

## Forensic Significance

### Intent to Conceal

Finding a download record in the WAL/Journal that is _missing_ from the main History file is strong evidence of anti-forensics (the user knowingly tried to hide the download).

### Time Gap

The WAL file can often give you a "buffer" of the last few hours or days of activity that haven't been permanently indexed yet.
