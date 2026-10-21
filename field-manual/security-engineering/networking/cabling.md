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

# Cabling

## Network Cabling Standards

Network cabling standards define the physical infrastructure that enables data transmission across computer networks. <mark style="color:$primary;">**These standards specify the construction, performance characteristics and maximum transmission speeds for different cable types.**</mark>

{% hint style="info" icon="ethernet" %}
Importance

Understanding cabling standards is essential as the physical layer (Layer 1) of the OSI model forms the foundation on which all network security depends. <mark style="color:$primary;">Weak or outdated cabling infrastructure can create vulnerabilities that compromise network integrity and performance.</mark>
{% endhint %}

***

## Transmission Media Types

Each medium carries a signal differently, and that decides how it handles interference, distance and eavesdropping.

<table><thead><tr><th width="150">Media</th><th>Signal</th><th>EMI / RFI Resistance</th><th>Eavesdropping Risk</th><th>Typical Use</th></tr></thead><tbody><tr><td><strong>UTP</strong> (Unshielded Twisted Pair)</td><td>Electrical (copper)</td><td><mark style="color:$danger;"><strong>Low</strong></mark>. Twisting cancels some interference.</td><td>High. Emits signals and is easy to tap.</td><td>Standard office cabling, patch leads, PoE.</td></tr><tr><td><strong>STP / FTP</strong> (Shielded / Foiled Twisted Pair)</td><td>Electrical (copper)</td><td><mark style="color:$warning;"><strong>Moderate–High</strong></mark>. Only if the shield is properly grounded.</td><td>Medium. Shield reduces emanations.</td><td>Copper runs near machinery or other EMI sources.</td></tr><tr><td><strong>Coaxial</strong></td><td>Electrical (copper)</td><td><mark style="color:$warning;"><strong>Moderate–High</strong></mark>. Braided shield around the conductor.</td><td>Medium. Vulnerable to vampire taps.</td><td>Legacy Ethernet, CCTV, cable TV and broadband.</td></tr><tr><td><strong>Fiber-Optic</strong></td><td>Light (glass or plastic)</td><td><mark style="color:$success;"><strong>Immune</strong></mark> to EMI, RFI, crosstalk and induced current.</td><td>Low. No emanations; tapping is difficult and potentially detectable.</td><td>Backbones, long runs, high-EMI or high-security areas.</td></tr><tr><td><strong>Wireless</strong></td><td>Radio waves</td><td><mark style="color:$danger;"><strong>Very Low</strong></mark>. Shared, noisy medium.</td><td>High. Anyone in range can capture traffic; relies on encryption.</td><td>Mobility and areas where cabling is impractical.</td></tr></tbody></table>

{% hint style="warning" %}
A shielded cable that is **not grounded** at the correct points can act as an antenna and make interference worse. STP only helps when installed correctly.
{% endhint %}

***

## Ethernet Categories (Twisted Pair)

The category rating system for <mark style="color:$primary;">**Unshielded Twisted Pair (UTP)**</mark> cable provides a standardised way to classify cables based on their construction quality and transmission capabilities. Each category represents improvements on shielding, twist rates and overall construction that enable higher data transmission speeds. <mark style="color:$primary;">**These improvements directly impact the reliability and speed of network communications.**</mark>

***

## Fiber-Optic Types

<table><thead><tr><th width="160"></th><th>Single-Mode (SMF)</th><th>Multi-Mode (MMF)</th></tr></thead><tbody><tr><td><strong>Core size</strong></td><td>Very small (~9 µm)</td><td>Larger (50 or 62.5 µm)</td></tr><tr><td><strong>Light source</strong></td><td>Laser</td><td>LED or VCSEL</td></tr><tr><td><strong>Distance</strong></td><td>Kilometres to tens of kilometres</td><td>Hundreds of metres</td></tr><tr><td><strong>Cost</strong></td><td>Higher optics cost</td><td>Cheaper optics</td></tr><tr><td><strong>Typical use</strong></td><td>Campus links, WAN, between buildings</td><td>Inside buildings and data centres</td></tr><tr><td><strong>Grades / jacket colour</strong></td><td>OS1/OS2 (yellow)</td><td>OM1/OM2 (orange), OM3/OM4 (aqua; OM4 sometimes violet), OM5 (lime green)</td></tr></tbody></table>

Common connectors: **LC** (small, most common today), **SC** (square, push-pull), **ST** (bayonet, legacy) and **MPO/MTP** (multi-fibre, high-density).

***

## Signal Degradation

Understanding why signals degrade explains why some media are chosen for hostile environments.

<table><thead><tr><th width="200">Factor</th><th>What Happens</th><th>Affects</th></tr></thead><tbody><tr><td><strong>Attenuation</strong></td><td>The signal weakens over distance (measured in dB). This is why copper Ethernet is limited to about 100 m per run.</td><td>All media. Far lower in fiber.</td></tr><tr><td><strong>Crosstalk</strong></td><td>Signal bleeds between adjacent wire pairs (NEXT near-end, FEXT far-end) or between neighbouring cables (alien crosstalk).</td><td>Copper only.</td></tr><tr><td><strong>EMI / RFI</strong></td><td>External electromagnetic or radio noise corrupts the signal. Sources include motors, generators, transformers, fluorescent lighting, power cables and radio transmitters.</td><td>Copper and wireless.</td></tr><tr><td><strong>Power fluctuations &#x26; ground loops</strong></td><td>Large electrical changes induce current on copper data lines, corrupting frames or damaging NICs and switch ports. Ground loops form when buildings or equipment sit at different ground potentials.</td><td>Copper only. Fiber breaks the electrical path.</td></tr><tr><td><strong>Dispersion</strong></td><td>Light pulses spread out over distance (modal dispersion is greatest in multi-mode), limiting speed and length.</td><td>Fiber.</td></tr><tr><td><strong>Physical damage</strong></td><td>Kinks, crushing, exceeding bend radius, poor terminations.</td><td>All cabled media. Fiber is especially sensitive to tight bends.</td></tr></tbody></table>

<mark style="color:$info;">**Implementation Example:**</mark> Keep copper data cabling away from power cables and EMI sources. Where they must meet, cross at 90° rather than running in parallel.

For protecting the facility itself from power problems (UPS, generators, surge protection), see [Physical & Environmental Security](../physical-and-environmental-security.md).

***

## Physical Security of Cabling

Cabling is part of the security boundary, not just infrastructure.

* **Copper emanations:** copper cables radiate electromagnetic signals that specialised equipment can capture without touching the cable.
* **Copper tapping:** copper can be tapped by splicing in, or for coax by a **vampire tap** that pierces the jacket to reach the conductor.
* **Fiber tapping:** fiber emits no electromagnetic signal. Tapping it means splicing into the glass or bending it to leak light. Both cause some signal loss, which active monitoring or an OTDR (optical time-domain reflectometer) can detect, though a skilled tap may only cause a small loss.
* **Protected Distribution Systems (PDS):** sensitive runs are placed in locked conduit or secured trays, with regular physical inspection.
* **Access to the cable plant:** wiring closets, patch panels and comms rooms are locked, and unused wall ports are disabled at the switch.
* **Documentation:** cables and ports are labelled and an up-to-date cabling map is maintained, so unauthorised additions stand out.

***

## Fire & Jacket Ratings

Cable jackets burn and produce smoke, so where a cable can be installed depends on its fire rating.

### US (NEC): Tested on the SSCP

<table><thead><tr><th width="160">Rating</th><th>Use</th></tr></thead><tbody><tr><td><strong>CMP</strong> (Plenum)</td><td>Air-handling spaces such as above suspended ceilings and below raised floors. Low smoke and low toxicity, so smoke isn't spread through the building's air supply. Highest rating.</td></tr><tr><td><strong>CMR</strong> (Riser)</td><td>Vertical shafts between floors. Resists fire spreading upwards, but is <strong>not</strong> suitable for plenum spaces.</td></tr><tr><td><strong>CM / CMG</strong> (General)</td><td>General horizontal runs within a single floor.</td></tr></tbody></table>

A higher rating can always replace a lower one (CMP → CMR → CM), but never the other way round.

### UK / EU

* UK and EU cabling is classified under the **Construction Products Regulation (CPR)** using **Euroclasses** (Aca, B1ca, B2ca, Cca, Dca, Eca, Fca), with extra ratings for smoke (**s**), flaming droplets (**d**) and acidity (**a**).
* **LSZH** (Low Smoke Zero Halogen) jackets are common in the UK. They produce little smoke and no toxic halogen gases when burning.
* UK installation guidance (BS 6701) sets minimum CPR classes, so check the current edition for specific requirements.

***

## Choosing Media

<table><thead><tr><th width="260">Environment / Requirement</th><th width="160">Best Choice</th><th>Why</th></tr></thead><tbody><tr><td>Heavy EMI and power fluctuations, little degradation tolerated</td><td><mark style="color:$success;"><strong>Fiber</strong></mark></td><td>Light is unaffected by EMI and there is no electrical path for induced current.</td></tr><tr><td>Long distance or between buildings</td><td><strong>Single-mode fiber</strong></td><td>Lowest attenuation; also avoids ground loops between buildings.</td></tr><tr><td>High-security or sensitive runs</td><td><strong>Fiber</strong> in a PDS</td><td>No emanations and tapping is difficult to do unnoticed.</td></tr><tr><td>Moderate EMI where copper is required (e.g. PoE)</td><td><strong>STP / FTP</strong></td><td>Shielding reduces interference, if properly grounded.</td></tr><tr><td>Standard office desks</td><td><strong>UTP</strong> (Cat6 / Cat6a)</td><td>Cheap, easy to install, supports PoE.</td></tr><tr><td>Legacy video or broadband feed</td><td><strong>Coax</strong></td><td>Existing infrastructure.</td></tr><tr><td>Mobility or no cabling possible</td><td><strong>Wireless</strong></td><td>Flexible, but needs strong encryption (WPA3) and suffers from interference.</td></tr></tbody></table>

{% hint style="success" %}
**Exam tip:** if a question mentions **EMI, power fluctuations, long distances, eavesdropping or tapping**, the answer is almost always **fiber**. Wireless is the worst choice for both interference and interception.
{% endhint %}
