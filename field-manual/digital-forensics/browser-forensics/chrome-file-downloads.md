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

# Chrome File Downloads

Chrome tracks all user downloads in the History database. This is vital for tracing the "lineage" of a file, identifying the specific URL a malicious payload originated from and confirming if the download was successful.

***

## Analysis Step

{% stepper %}
{% step %}
#### Acquisition

Close Chrome before copying the `History` file as Chrome locks the database while open.
{% endstep %}

{% step %}
#### Verify Integrity

Check the `Bytes Received`. If it matches the expected file size, the download likely finished.
{% endstep %}

{% step %}
#### Cross-Reference

Match the `Start Time` with Windows Event Logs (Event ID 11 for File Create) to see if the file was executed immediately after download.
{% endstep %}
{% endstepper %}

***

## File Location

The database is a SQLite file located at:

`C:\Users\[USER]\AppData\Local\Google\Chrome\User Data\Default\History`

{% hint style="info" %}
#### Note

If the user has multiple Chrome profiles, the folder `Default` may be named `Profile 1`, `Profile 2`, etc.
{% endhint %}

***

## Key Database Tables

To extract download data, we need to query two specific tables within the `History` database:

* `downloads`: Contains file paths, timestamps, and file sizes.
* `downloads_url_chains`: Maps the download to its source URL (including redirects).

***

## Forensic SQL Query

If we are using a tool like [db-browser-for-sqlite.md](../../../toolbox/tooling/utilities/db-browser-for-sqlite.md "mention") or a PowerShell SQLite wrapper, use the following query to correlate the file name with its source:

```sql
SELECT 
    datetime(downloads.start_time/1000000-11644473600, 'unixepoch') AS "Start Time",
    downloads.target_path AS "File Path",
    downloads_url_chains.url AS "Source URL",
    downloads.received_bytes AS "Bytes Received",
    CASE downloads.state WHEN 1 THEN 'Complete' WHEN 2 THEN 'Cancelled' ELSE 'Interrupted' END AS "Status"
FROM downloads
JOIN downloads_url_chains ON downloads.id = downloads_url_chains.id
ORDER BY "Start Time" DESC;
```

***

## Forensic Significance

### URL Chains

This table is unique because it shows the entire redirect path. If a user clicked a shortened bit.ly link that redirected to a malicious S3 bucket, both URLs will be recorded here.

### Target Path vs. Current Path

The `target_path` shows where the user intended to save the file. If the file is missing from that location, it may have been moved, deleted, or quarantined by an EDR.

### Referrer URL

This helps identify the website the user was visiting before the download started (e.g., a spear-phishing landing page).
