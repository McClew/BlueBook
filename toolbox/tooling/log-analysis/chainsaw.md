# Chainsaw

{% hint style="info" %}
#### Download & Install

[https://github.com/WithSecureLabs/chainsaw](https://github.com/WithSecureLabs/chainsaw)
{% endhint %}

***

## Cheatsheet

{% tabs %}
{% tab title="Common (Win)" %}
<table><thead><tr><th width="692">Command</th><th data-hidden>Description</th></tr></thead><tbody><tr><td><code>.\chainsaw.exe hunt .\&#x3C;log_collection_dir> -s .\sigma --mapping mappings/sigma-event-logs-all.yml</code></td><td></td></tr></tbody></table>
{% endtab %}

{% tab title="Output & Formatting" %}
<table><thead><tr><th width="231">Flag</th><th>Description</th></tr></thead><tbody><tr><td><code>-o, --output &#x3C;output></code></td><td>"A path to output results to" and will automatically adjust output type based on the format flags provided.</td></tr><tr><td><code>--json</code></td><td>"Print the output in json format"</td></tr><tr><td><code>--csv</code></td><td>"Print the output in csv format"</td></tr><tr><td><code>--log</code></td><td>"Print the output in log like format"</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

***

## Methods

### Searching

The chainsaw `search` option should be utilised for targeted operations. For example, if we have a specific Indicator of Compromise (IOC) - like an IP address, username, or a known malicious file hash - and need find every instance.

* Logic: String matching and Regular Expressions.
* Key Strength: Speed. It is the fastest way to sift through gigabytes of logs for a single keyword.

Key Parameters:

* `-e` or `--event-id`: Filter by specific Windows Event IDs.
* `-t` or `--string`: Search for a specific string.
* `-r` or `--regex`: Use complex patterns to match data.

Example:

{% code title="Search for a specific IP address" %}
```bash
chainsaw search "192.168.1.50" --json ./logs/
```
{% endcode %}

### Hunting

The `hunt` option should be used when conducting a proactive, broad-spectrum operation. Instead of looking for a specific word, we are applying a library of Sigma Rules that match against known indicators.

* Logic: Rule-based detection (Sigma YAML files).
* Key Strength: Pattern recognition. It can find complex attacks that a simple string search would miss (like Kerberoasting or Brute Force attempts).

Key Parameters:&#x20;

* `-s` or `--sigma`: Point to a directory of Sigma rules.
* `-m` or `--mapping`: Uses a mapping file to tell Chainsaw how to translate Sigma logic to the specific logs you've provided.

Example:

{% code title="Hunt for all known threats using Sigma rules" %}
```bash
chainsaw hunt ./logs/ -s ./sigma_rules/ --mapping ./mappings/sigma-event-logs-all.yml
```
{% endcode %}

### Analysis

While `search` and `hunt` look at Event Logs, the `analyse` subcommand is a specialised forensic feature. It is currently focused on high-value artifacts like Shimcache, Amcache, and the SRUM (System Resource Usage Monitor) database.

* Logic: Artifact parsing and timestamp enrichment.
* When to use: When we need to reconstruct a timeline of when an executable was first run or how much data a process sent over the network.
* Key Strength: Context. It takes raw, difficult-to-read binary artifacts and turns them into a human-readable timeline.
