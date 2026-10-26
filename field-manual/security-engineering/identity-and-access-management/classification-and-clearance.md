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
  anchors:
    visible: true
---

# Classification & Clearance

Classification and clearance are the label system that [access-control.md](access-control.md "mention") [Mandatory-Access-Control (MAC)](access-control.md#mandatory-access-control-mac) enforces. The system compares the <mark style="color:$primary;">**clearance**</mark> held by a subject against the <mark style="color:$primary;">**classification**</mark> of an object, and grants or denies access. Neither the user nor the data owner can override the decision.

***

## Core Vocabulary

<table><thead><tr><th width="180">Term</th><th>Meaning</th></tr></thead><tbody><tr><td><strong>Subject</strong></td><td>The active entity requesting access (a user or a process). Subjects hold a <strong>clearance</strong>.</td></tr><tr><td><strong>Object</strong></td><td>The passive entity being accessed (a file, record, or system). Objects hold a <strong>classification</strong>.</td></tr><tr><td><strong>Clearance</strong></td><td>A formal statement that a subject is <em>trustworthy</em> enough to handle information up to a given level, granted after vetting.</td></tr><tr><td><strong>Classification</strong></td><td>A level assigned to an object according to the damage its disclosure would cause.</td></tr><tr><td><strong>Security Label</strong></td><td>A classification level <strong>plus</strong> a set of categories, e.g. <code>SECRET {NUCLEAR, CRYPTO}</code>.</td></tr><tr><td><strong>Need-to-Know</strong></td><td>A requirement that the subject's role actually needs the information, regardless of clearance.</td></tr></tbody></table>

{% hint style="info" %}
A security label has **two parts**: a hierarchical **level** and a non-hierarchical set of **categories** (compartments).
{% endhint %}

***

## Classification Schemes

### US Government / Military

This is the scheme ISC2 tests. Each level is defined by the damage unauthorised disclosure would cause to national security.

<table><thead><tr><th width="180">Level</th><th>Damage if Disclosed</th></tr></thead><tbody><tr><td><mark style="color:$danger;"><strong>Top Secret</strong></mark></td><td><em>Exceptionally grave</em> damage</td></tr><tr><td><mark style="color:$warning;"><strong>Secret</strong></mark></td><td><em>Serious</em> damage</td></tr><tr><td><mark style="color:$info;"><strong>Confidential</strong></mark></td><td><em>Damage</em></td></tr><tr><td><mark style="color:$success;"><strong>Unclassified</strong></mark></td><td>No damage to national security. May still be Sensitive But Unclassified (SBU) or Controlled Unclassified Information (CUI).</td></tr></tbody></table>

{% hint style="success" icon="brain-circuit" %}
#### Memory Aid

The damage wording drops one word at each level: _exceptionally grave_ → _serious_ → _damage_ → _none_.
{% endhint %}

### Commercial / Private Sector

<table><thead><tr><th width="220">Level</th><th>Typical Content</th></tr></thead><tbody><tr><td><mark style="color:$danger;"><strong>Confidential / Proprietary</strong></mark></td><td>Trade secrets, source code, M&#x26;A plans. Highest commercial level.</td></tr><tr><td><mark style="color:$warning;"><strong>Private</strong></mark></td><td>Personal data about employees or customers (HR records, medical data).</td></tr><tr><td><mark style="color:$info;"><strong>Sensitive</strong></mark></td><td>Internal data needing protection from unauthorised modification, e.g. financial forecasts.</td></tr><tr><td><mark style="color:$success;"><strong>Public</strong></mark></td><td>Approved for release; disclosure causes no harm.</td></tr></tbody></table>

{% hint style="warning" %}
"Private" in the commercial scheme refers to **personal** information, not simply "not public".
{% endhint %}

### UK Government Security Classifications

Not tested on the SSCP, but relevant to UK work. Keep it separate from the US scheme in your head.

<table><thead><tr><th width="220">Level</th><th>Typical Content</th></tr></thead><tbody><tr><td><mark style="color:$info;"><strong>OFFICIAL</strong></mark></td><td>The majority of routine public-sector information. <strong>OFFICIAL-SENSITIVE</strong> is a handling marking within OFFICIAL, not a separate level.</td></tr><tr><td><mark style="color:$warning;"><strong>SECRET</strong></mark></td><td>Information needing heightened protection against capable threat actors.</td></tr><tr><td><mark style="color:$danger;"><strong>TOP SECRET</strong></mark></td><td>The most sensitive information, protected against the highest threats.</td></tr></tbody></table>

***

## Clearance & Need-to-Know

<mark style="color:$primary;">Clearance answers</mark> <mark style="color:$primary;"></mark>_<mark style="color:$primary;">"Can this person be trusted with information at this level?"</mark>_

<mark style="color:$primary;">Need-to-know answers</mark> <mark style="color:$primary;"></mark>_<mark style="color:$primary;">"Does this person's job actually require this information?"</mark>_

<mark style="color:red;">Both must be true for access to be granted.</mark>

<mark style="color:$info;">**Implementation Example:**</mark> An analyst with Top Secret clearance working on a naval project cannot read a Top Secret file about an unrelated aircraft programme. They are cleared for the level but have no need-to-know.

### Compartments & Categories

Compartments (also called categories, or caveats) enforce need-to-know **within** a level. Sensitive Compartmented Information (SCI) is the classic US example: access requires both the clearance level **and** formal read-in to the specific compartment.

### UK Vetting Levels (Reference)

* <mark style="color:$info;">**BPSS**</mark><mark style="color:$info;">:</mark> Baseline Personnel Security Standard, pre-employment checks.
* <mark style="color:$info;">**CTC**</mark><mark style="color:$info;">:</mark> Counter-Terrorist Check.
* <mark style="color:$info;">**SC**</mark><mark style="color:$info;">:</mark> Security Check, for regular access to <mark style="color:$warning;">SECRET</mark>.
* <mark style="color:$info;">**DV**</mark><mark style="color:$info;">:</mark> Developed Vetting, for regular access to <mark style="color:red;">TOP SECRET</mark>.

***

## Dominance & Lattice-Based Access

A subject's label **dominates** an object's label only when **both** conditions are met:

1. The subject's **level ≥** the object's level, **and**
2. The subject's **categories ⊇** (are a superset of) the object's categories.

### Worked Example

A subject is cleared at `SECRET {A, B}`. Which objects can they read?

{% stepper %}
{% step %}
#### Object: CONFIDENTIAL {A}

Level: Secret ≥ Confidential <i class="fa-check" style="color:$success;">:check:</i>. Categories: {A, B} ⊇ {A} <i class="fa-check" style="color:$success;">:check:</i>.

<mark style="color:$success;">**Access granted.**</mark>
{% endstep %}

{% step %}
#### Object: CONFIDENTIAL {C}

Level: Secret ≥ Confidential <i class="fa-check" style="color:$success;">:check:</i>. Categories: {A, B} does not contain C <i class="fa-xmark" style="color:$danger;">:xmark:</i>.

<mark style="color:$danger;">**Access denied.**</mark> No need-to-know for compartment C, even though the level is lower.
{% endstep %}

{% step %}
#### Object: TOP SECRET {A}

Level: Secret < Top Secret <i class="fa-xmark" style="color:$danger;">:xmark:</i>.

<mark style="color:$danger;">**Access denied.**</mark> Clearance is too low, even though the category matches.
{% endstep %}

{% step %}
#### Object: SECRET {A, B}

Level equal <i class="fa-check" style="color:$success;">:check:</i>. Categories equal <i class="fa-check" style="color:$success;">:check:</i>.

<mark style="color:$success;">**Access granted.**</mark> Equal labels dominate each other.
{% endstep %}
{% endstepper %}

### Lattice-Based Access Control

When levels and categories are combined, the full set of possible labels forms a **lattice**: a partially ordered structure where some labels can be compared and others cannot (e.g. `SECRET {A}` and `SECRET {B}` are incomparable; neither dominates the other).

* <mark style="color:$info;">**Least Upper Bound (LUB):**</mark> the lowest label that dominates both of two labels. For `SECRET {A}` and `CONFIDENTIAL {B}` it is `SECRET {A, B}`.
* <mark style="color:$info;">**Greatest Lower Bound (GLB):**</mark> the highest label that both labels dominate. For `SECRET {A, B}` and `TOP SECRET {B, C}` it is `SECRET {B}`.

***

## Security Modes of Operation

The mode describes how a system handles users with different clearances and data at different levels. Each mode relaxes one more requirement than the one above it.

<table><thead><tr><th width="160">Mode</th><th>All users cleared for…</th><th>Formal approval for…</th><th>Need-to-know for…</th></tr></thead><tbody><tr><td><strong>Dedicated</strong></td><td>All data</td><td>All data</td><td>All data</td></tr><tr><td><strong>System High</strong></td><td>All data</td><td>All data</td><td><mark style="color:$warning;">Some data</mark></td></tr><tr><td><strong>Compartmented</strong></td><td>All data</td><td><mark style="color:$warning;">Some data</mark></td><td><mark style="color:$warning;">Some data</mark></td></tr><tr><td><strong>Multilevel</strong></td><td><mark style="color:$warning;">Some data</mark></td><td><mark style="color:$warning;">Some data</mark></td><td><mark style="color:$warning;">Some data</mark></td></tr></tbody></table>

{% hint style="success" icon="brain-circuit" %}
#### Memory Aid

Read the table from the right-hand column leftwards. _Need-to-know_ is relaxed first (System High), then _formal approval_ (Compartmented), then _clearance_ (Multilevel). Only Multilevel relies on the system itself to separate users who are not cleared for everything.
{% endhint %}

***

## Enforcement Rules

The two formal models most often paired with classification are opposites of each other.

### Bell-LaPadula (Confidentiality)

* **Simple Security Property:** _no read up_. A subject cannot read an object at a higher level.
* **\* (Star) Property:** _no write down_. A subject cannot write to an object at a lower level.
* **Strong \* Property:** a subject can read and write only at its own level.

<mark style="color:$info;">**Why no write down?**</mark> It stops a Top Secret user (or malware running as them) copying Top Secret data into an Unclassified file.

### Biba (Integrity)

* **Simple Integrity Property:** _no read down_. A subject cannot read lower-integrity data that might contaminate it.
* **\* Integrity Property:** _no write up_. A subject cannot write to a higher-integrity object.
* **Invocation Property:** a subject cannot invoke (request service from) a subject at a higher integrity level.

{% hint style="success" %}
**Memory aid:** Biba is Bell-LaPadula flipped upside down. BLP protects **secrets** (confidentiality); Biba protects **trust** (integrity). Neither model addresses availability.
{% endhint %}

***

## Classification Lifecycle & Roles

### Roles

<table><thead><tr><th width="160">Role</th><th>Responsibility</th></tr></thead><tbody><tr><td><strong>Data Owner</strong></td><td>Senior person accountable for the data. <strong>Assigns</strong> the classification and approves access.</td></tr><tr><td><strong>Data Custodian</strong></td><td>Typically IT. <strong>Implements</strong> the controls the classification requires (backups, permissions, encryption).</td></tr><tr><td><strong>User</strong></td><td>Follows handling rules for the classification.</td></tr></tbody></table>

### Lifecycle

1. **Classify:** the owner assigns a level when the data is created or acquired.
2. **Mark & Label:** apply visible markings (headers, footers, cover sheets) and system labels (metadata) so the classification travels with the data.
3. **Handle & Store:** apply the storage, transmission and access requirements for that level.
4. **Review:** reassess periodically. Sensitivity usually decreases over time.
5. **Declassify / Downgrade:** a formal, authorised and audited process. Never done ad hoc by a user.
6. **Destroy:** sanitise or destroy media to the standard the classification requires.

### Aggregation & Inference

* **Aggregation:** combining several pieces of lower-classified data produces information that is more sensitive than any single piece (e.g. individual troop movements vs. the full deployment plan).
* **Inference:** deducing higher-classified information from lower-classified data you can access.
* **Countermeasure:** **polyinstantiation**, where a database holds multiple versions of a record at different classification levels so lower-cleared users see a cover version rather than an obvious gap.
