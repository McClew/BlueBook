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

# Portable Executables

Windows operating systems employ the `Portable Executable (PE)` format to encapsulate executable programs, `DLLs (Dynamic Link Libraries)`, and other integral system components. In the realm of malware analysis, an intricate understanding of the PE file format is indispensable. It allows us to gain significant insights into the executable's structure, operations, and potential malign activities embedded within the file.

PE files accommodate a wide variety of data types including `executables (.exe)`, `dynamic link libraries (.dll)`, `kernel modules (.sys)`, `control panel applications (.cpl)`, and many more. The PE file format is fundamentally a data structure containing the vital information required for the Windows OS loader to manage the executable code, effectively loading it into memory.

***

## PE Sections <a href="#pe-sections" id="pe-sections"></a>

The PE Structure also houses a `Section Table`, an element comprising several sections dedicated to distinct purposes. The sections are essentially the repositories where the actual content of the file, including the data, resources utilised by the program, and the executable code, is stored. The `.text` section is often under scrutiny for potential artifacts related to injection attacks.

Common PE sections include:

* `Text Section (.text)`: The hub where the executable code of the program resides.
* `Data Section (.data)`: A storage for initialised global and static data variables.
* `Read-only initialized data (.rdata)`: Houses read-only data such as constant values, string literals, and initialised global and static variables.
* `Exception information (.pdata)`: A collection of function table entries utilised for exception handling.
* `BSS Section (.bss)`: Holds uninitialised global and static data variables.
* `Resource Section (.rsrc)`: Safeguards resources such as images, icons, strings, and version information.
* `Import Section (.idata)`: Details about functions imported from other DLLs.
* `Export Section (.edata)`: Information about functions exported by the executable.
* `Relocation Section (.reloc)`: Details for relocating the executable's code and data when loaded at a different memory address.

We can visualise the sections of a portable executable using a tool like `pestudio` as demonstrated below.

<figure><img src="../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Delving into the Portable Executable (PE) file format is pivotal for malware analysis, offering insights into the file's structure, code analysis, import and export functions, resource analysis, anti-analysis techniques, and extraction of indicators of compromise. Our comprehension of this foundation paves the way for efficacious malware analysis.

***

## Section Hashing <a href="#section-hashing-hashing-pe-sections" id="section-hashing-hashing-pe-sections"></a>

Section hashing, is a technique that allows analysts to identify sections of a Portable Executable (PE) file that have been modified. This can be particularly useful for identifying minor variations in malware samples, a common tactic employed by attackers to evade detection.

The Section Hashing technique works by calculating the cryptographic hash of each of these sections. When comparing two PE files, if the hash of corresponding sections in the two files matches, it suggests that the particular section has not been modified between the two versions of the file.

By applying section hashing, security analysts can identify parts of a PE file that have been tampered with or altered. This can help identify similar malware samples, even if they have been slightly modified to evade traditional signature-based detection methods.

Tools such as `pefile` in Python can be used to perform `section hashing`. In Python, for example, you can use the pefile module to access and hash the data in individual sections of a PE file as follows.

{% code title="section_hashing.py" lineNumbers="true" %}
```python
import sys
import pefile
pe_file = sys.argv[1]
pe = pefile.PE(pe_file)
for section in pe.sections:
    print (section.Name, "MD5 hash:", section.get_hash_md5())
    print (section.Name, "SHA256 hash:", section.get_hash_sha256())

```
{% endcode %}

Remember that while section hashing is a powerful technique, it is not foolproof. Malware authors might employ tactics like section name obfuscation or dynamically generating section names to try and bypass this kind of analysis.

```bash
python3 section_hashing.py <FILE_PATH>
b'.text\x00\x00\x00' MD5 hash: c7613102e2ecec5dcefc144f83189153
b'.text\x00\x00\x00' SHA256 hash: 7609ecc798a357dd1a2f0134f9a6ea06511a8885ec322c7acd0d84c569398678
b'.rdata\x00\x00' MD5 hash: d8037d744b539326c06e897625751cc9
b'.rdata\x00\x00' SHA256 hash: 532e9419f23eaf5eb0e8828b211a7164cbf80ad54461bc748c1ec2349552e6a2
b'.data\x00\x00\x00' MD5 hash: 22a8598dc29cad7078c291e94612ce26
b'.data\x00\x00\x00' SHA256 hash: 6f93fb1b241a990ecc281f9c782f0da471628f6068925aaf580c1b1de86bce8a
b'.rsrc\x00\x00\x00' MD5 hash: 12e1bd7375d82cca3a51ca48fe22d1a9
b'.rsrc\x00\x00\x00' SHA256 hash: 1efe677209c1284357ef0c7996a1318b7de3836dfb11f97d85335d6d3b8a8e42
```
