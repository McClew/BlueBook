# Data Sensitivity & Regulation

Data sensitivity and regulation decide where cryptography is applied and how strong it must be. Sensitivity is the internal driver: the impact if data is disclosed, altered or lost. Regulation is the external driver: the minimum the organisation must meet regardless of its own risk appetite.

{% hint style="info" %}
Most regulations are written around a type of data. You can't choose or evidence controls until you know what data you hold, where it lives and how it moves.
{% endhint %}

***

## Data Classification

Classification assigns a label to data based on the impact of a loss of confidentiality, integrity or availability. Each label maps to handling rules, including when encryption is required.

<mark style="color:$info;">**Data Owner:**</mark> Senior business role accountable for the data. Sets its classification and approves access.

<mark style="color:$info;">**Data Custodian:**</mark> Usually IT or security. Implements the controls the classification requires (encryption, backups, key management).

<mark style="color:$info;">**Controller / Processor:**</mark> Privacy law terms. The controller decides why and how personal data is processed; the processor acts on its instructions.

### Common Schemes

| Scheme        | Levels (low → high)                                           |
| ------------- | ------------------------------------------------------------- |
| Commercial    | Public → Internal → Confidential → Restricted                 |
| UK Government | OFFICIAL (incl. OFFICIAL-SENSITIVE) → SECRET → TOP SECRET     |
| US Government | Unclassified (incl. CUI) → Confidential → Secret → Top Secret |

### Setting the Level

<mark style="color:$info;">**Impact:**</mark> FIPS 199 rates confidentiality, integrity and availability as low, moderate or high. The highest rating sets the overall level (high-water mark).

<mark style="color:$info;">**Aggregation:**</mark> Individually harmless data can become sensitive when combined (name vs name + date of birth + address).

<mark style="color:$info;">**Declassification:**</mark> Sensitivity changes over time. Owners should review labels and downgrade where appropriate.

### States of Data

| State      | Typical Cryptographic Control                                                                 |
| ---------- | --------------------------------------------------------------------------------------------- |
| At rest    | Full-disk, volume, database (TDE) or field-level encryption; slow salted hashes for passwords |
| In transit | TLS 1.2+ (prefer 1.3), IPsec/VPN, SSH/SFTP, S/MIME or PGP                                     |
| In use     | Access control, confidential computing (secure enclaves)                                      |

<mark style="color:$info;">**Crypto-shredding:**</mark> Destroying the encryption keys so the data becomes unrecoverable. Often the only practical way to sanitise cloud storage and SSDs.

***

## Sensitive Data Types

### Personally Identifiable Information (PII)

Any information that identifies a living person, directly or indirectly. UK GDPR calls it **personal data** and defines it more broadly than the US term.

<mark style="color:$info;">**Direct Identifiers:**</mark> Name, email, phone number, NI number, passport number.

<mark style="color:$info;">**Indirect Identifiers:**</mark> IP address, device or cookie ID, location, combinations such as postcode + date of birth.

<mark style="color:$info;">**Special Category (Art. 9):**</mark> Racial or ethnic origin, political opinions, religious beliefs, trade union membership, genetic and biometric data, health, sex life and sexual orientation. Requires a stronger legal basis and stronger protection.

<mark style="color:$info;">**Pseudonymisation:**</mark> Replacing identifiers with tokens or keyed hashes, with the re-identification key held separately. Still personal data, but lower risk.

<mark style="color:$info;">**Anonymisation:**</mark> Irreversibly removing the link to a person. Falls outside data protection law, but is hard to achieve.

{% hint style="warning" %}
An unsalted hash of an email address is not anonymous. It can be reversed by hashing a list of known emails and comparing.
{% endhint %}

### Protected Health Information (PHI)

A US HIPAA term: identifiable health information held by a **covered entity** (provider, health plan, clearing house) or its **business associates**. Electronic PHI is **ePHI**.

<mark style="color:$info;">**Identifiers:**</mark> HIPAA lists 18, including names, dates (other than year), contact details, record numbers, biometrics and full-face photos.

<mark style="color:$info;">**De-identification:**</mark> Removing all 18 identifiers (Safe Harbor) or expert determination takes data out of HIPAA scope.

<mark style="color:$info;">**UK Equivalent:**</mark> No PHI category. Health data is special category personal data under UK GDPR; NHS bodies add the Data Security and Protection Toolkit (DSPT).

### Cardholder Data

Governed by contract through PCI DSS, which calls it **account data**. The PAN is what brings a system into the cardholder data environment (CDE).

| Category                            | Elements                                           | Storage After Authorisation                  |
| ----------------------------------- | -------------------------------------------------- | -------------------------------------------- |
| Cardholder Data (CHD)               | PAN, cardholder name, expiry date, service code    | Allowed if protected; PAN must be unreadable |
| Sensitive Authentication Data (SAD) | Full track/chip data, CVV2/CVC2, PIN and PIN block | Never, even if encrypted                     |

### Intellectual Property (IP)

Trade secrets, source code, designs, formulas, research, pricing and M\&A plans. Rarely has a regulator; protection is driven by business impact, contracts and NDAs.

<mark style="color:$info;">**Trade Secrets:**</mark> Only legally protected if the owner takes reasonable steps to keep them secret. Encryption and access control are evidence of those steps.

<mark style="color:$info;">**Controls:**</mark> Repository and backup encryption, DRM/IRM (encryption plus usage rules), code signing, watermarking.

### Credentials & Secrets

Passwords are stored with slow salted hashing (Argon2id, bcrypt, scrypt, PBKDF2), never reversible encryption. API keys, private keys and tokens belong in a vault or HSM, not in code.

***

## Regulations & Standards

<mark style="color:$info;">**Law:**</mark> Mandatory and enforced by a regulator (UK GDPR, HIPAA).

<mark style="color:$info;">**Contractual:**</mark> Mandatory because a contract says so (PCI DSS).

<mark style="color:$info;">**Voluntary:**</mark> Best practice adopted or certified against (ISO/IEC 27001, NIST). Becomes mandatory once a customer requires it.

{% hint style="info" %}
Most of these require "strong cryptography" or "appropriate measures" rather than naming algorithms. Current NIST and NCSC guidance fills the gap.
{% endhint %}

### PCI DSS v4.0.1

<mark style="color:$info;">**Applies To:**</mark> Anyone storing, processing or transmitting cardholder data, or able to affect its security.

<mark style="color:$info;">**Status:**</mark> Only active version since v4.0 retired on 31 December 2024. Future-dated requirements became mandatory on 31 March 2025.

| Requirement | Summary                                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------ |
| 3.2–3.3     | Minimise stored account data. Never store SAD after authorisation.                                           |
| 3.4         | Mask displayed PAN (max first six / last four).                                                              |
| 3.5         | Render stored PAN unreadable: keyed hashes, truncation, tokens or strong encryption.                         |
| 3.5.1.1     | Hashes of PAN must be keyed (e.g. HMAC). Plain hashes are brute-forceable.                                   |
| 3.5.1.2     | Disk-level encryption only satisfies 3.5 for removable media.                                                |
| 3.6–3.7     | Key management: protect and minimise key storage, cryptoperiods, rotation, split knowledge and dual control. |
| 4.2.1       | Strong crypto for PAN over public networks; only valid, unexpired certificates.                              |
| 4.2.1.1     | Inventory of trusted keys and certificates.                                                                  |
| 4.2.2       | Secure PAN in end-user messaging (email, chat), or don't send it.                                            |
| 12.3.3      | Review cipher suites and protocols at least every 12 months.                                                 |

<mark style="color:$info;">**In Practice:**</mark> TLS 1.2+ with strong ciphers. SSL and TLS 1.0/1.1 fail. Tokenisation through the payment provider removes most systems from scope.

### ISO/IEC 27001 / 27002:2022

Risk-based ISMS standard. Controls are selected in the Statement of Applicability.

| Control     | Relevance                                                               |
| ----------- | ----------------------------------------------------------------------- |
| 5.12 / 5.13 | Classification and labelling of information                             |
| 5.14        | Information transfer                                                    |
| 5.31        | Legal and regulatory requirements, including crypto import/export laws  |
| 5.34        | Privacy and protection of PII                                           |
| 8.24        | Use of cryptography, including key management and a cryptography policy |

<mark style="color:$info;">**Related:**</mark> ISO/IEC 27701 (privacy), 27018 (PII in cloud), 19790 (crypto modules), 11770 (key management), 18033 (encryption algorithms).

### UK GDPR & DPA 2018

<mark style="color:$info;">**Art. 5(1)(f):**</mark> Integrity and confidentiality principle.

<mark style="color:$info;">**Art. 25:**</mark> Data protection by design and by default.

<mark style="color:$info;">**Art. 32:**</mark> Security of processing. Names pseudonymisation and encryption as appropriate measures.

<mark style="color:$info;">**Art. 33:**</mark> Notify the ICO within 72 hours unless the breach is unlikely to result in risk.

<mark style="color:$info;">**Art. 34(3)(a):**</mark> No need to notify individuals if the data was unintelligible, e.g. encrypted and the key was not compromised.

### HIPAA (US)

<mark style="color:$info;">**Current Rule:**</mark> Encryption at rest and in transit is **addressable**: implement it, or document why an equivalent alternative is reasonable.

<mark style="color:$info;">**Safe Harbour:**</mark> PHI encrypted to HHS guidance (NIST SP 800-111, SP 800-52) is "secured"; losing it is not a reportable breach.

<mark style="color:$info;">**Pending:**</mark> A proposed update would make encryption mandatory. Not finalised; target date moved to July 2027.

### FIPS 140-3 (US)

Validation standard for cryptographic modules, with four security levels (Level 1 software through Level 4 tamper-responsive hardware). Required for US federal systems and common in defence, healthcare and finance contracts.

<mark style="color:$info;">**FIPS 140-2:**</mark> All certificates moved to the CMVP Historical List in September 2026. Check products claiming "FIPS validated" hold an active 140-3 certificate.

<mark style="color:$info;">**Related NIST:**</mark> SP 800-57 (key management), SP 800-131A (approved algorithms), SP 800-52 (TLS), FIPS 203/204/205 (post-quantum).

### Crypto Law & Export Controls

<mark style="color:$info;">**Export Controls:**</mark> Strong cryptography is dual-use under the Wassenaar Arrangement (UK Export Control Order 2008; US EAR). Mass-market products are usually exempt; HSMs and custom crypto may need a licence.

<mark style="color:$info;">**Key Disclosure:**</mark> RIPA 2000 Part III allows UK authorities to demand keys or decrypted data.

<mark style="color:$info;">**Data Sovereignty:**</mark> Where data and keys are held determines which law applies. BYOK/HYOK keeps key control in your chosen jurisdiction.

***

## Quick Reference

| Data Type                 | Driver                                 | Cryptographic Expectation                                                             |
| ------------------------- | -------------------------------------- | ------------------------------------------------------------------------------------- |
| Personal data             | UK GDPR Art. 32, ISO 27001             | Encrypt devices, databases and backups by risk; pseudonymise where possible; TLS 1.2+ |
| Special category / health | UK GDPR Art. 9, DSPT; HIPAA for US PHI | Encrypt by default; field-level for the most sensitive fields                         |
| Cardholder data           | PCI DSS v4.0.1                         | PAN unreadable everywhere; never store SAD; tokenise to reduce scope                  |
| Intellectual property     | Contracts, trade secret law            | Repository and backup encryption; DRM/IRM                                             |
| Credentials & keys        | ISO 27001 8.24, PCI DSS Req. 8         | Salted slow hashes; vault or HSM                                                      |

{% hint style="warning" %}
Compliance is a floor, not a ceiling. Full-disk encryption on a running server, TLS that terminates at the edge, and keys stored beside the data they protect all pass audits while protecting little.
{% endhint %}
