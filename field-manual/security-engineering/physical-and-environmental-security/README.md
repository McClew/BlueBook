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

# Physical & Environmental Security

Physical and environmental controls protect the facility and everything in it from power problems, heat, water, fire and electromagnetic threats. <mark style="color:$primary;">**If the power, cooling or building fails, every logical control fails with it.**</mark> These controls mainly protect <mark style="color:$success;">**availability**</mark>, with emanation security also protecting <mark style="color:$success;">**confidentiality**</mark>.

{% hint style="info" %}
For how network media themselves resist EMI and power fluctuations, see [networking](../networking/ "mention") > [cabling.md](../networking/cabling.md "mention").
{% endhint %}

***

## Power Protection

<table><thead><tr><th width="200">Control</th><th>Protects Against</th><th>Notes</th></tr></thead><tbody><tr><td><strong>Surge Protector</strong></td><td>Spikes, surges</td><td>Diverts excess voltage. Does nothing for low voltage or loss of power.</td></tr><tr><td><strong>Line / Power Conditioner</strong></td><td>Noise, sags, surges</td><td>Smooths and regulates the supply. No battery, so no protection from outages.</td></tr><tr><td><strong>UPS</strong></td><td>Short outages, sags, brownouts</td><td>Battery bridge long enough to shut down cleanly or for a generator to start.</td></tr><tr><td><strong>Generator</strong></td><td>Prolonged outages</td><td>Needs fuel supply, regular load testing and a UPS to cover its start-up time.</td></tr><tr><td><strong>Redundant Supply</strong></td><td>Single-point failures</td><td>Dual power supplies in devices, dual PDUs, and ideally dual feeds from separate substations.</td></tr></tbody></table>

### Power Anomalies

<table><thead><tr><th width="227">Condition</th><th width="259">Momentary</th><th>Prolonged</th></tr></thead><tbody><tr><td><strong>High voltage</strong></td><td><mark style="color:$warning;"><strong>Spike</strong></mark></td><td><mark style="color:$warning;"><strong>Surge</strong></mark></td></tr><tr><td><strong>Low voltage</strong></td><td><mark style="color:$info;"><strong>Sag / Dip</strong></mark></td><td><mark style="color:$info;"><strong>Brownout</strong></mark></td></tr><tr><td><strong>Loss of power</strong></td><td><mark style="color:$danger;"><strong>Fault</strong></mark></td><td><mark style="color:$danger;"><strong>Blackout</strong></mark></td></tr></tbody></table>

### Terminology

* <mark style="color:$info;">**Inrush current:**</mark> the initial surge drawn when equipment is switched on. Powering up many devices at once can trip breakers or cause a sag for everything else on the circuit.
* <mark style="color:$info;">**Noise:**</mark> EMI or RFI interference carried on the power line (transient noise), often from motors, fluorescent lighting or other equipment sharing the circuit.

### UPS Types

{% stepper %}
{% step %}
#### Standby (Offline)

Equipment runs on mains power. The UPS switches to battery when mains fails, with a short **transfer time**. Cheapest; least protection.
{% endstep %}

{% step %}
#### Line-Interactive

Regulates voltage continuously (handles sags and surges without using the battery), then switches to battery on outage. Common for small server rooms.
{% endstep %}

{% step %}
#### Online (Double-Conversion)

Equipment **always** runs from the inverter: AC is converted to DC and back to clean AC. **Zero transfer time** and full isolation from mains problems. Most expensive; best protection, used in data centres.
{% endstep %}
{% endstepper %}

{% hint style="warning" %}
#### <mark style="color:$warning;">A UPS is not long-term power</mark>

Its job is to bridge the gap until the generator takes over, or to allow a controlled shutdown.
{% endhint %}

***

## Environmental Controls

### Temperature

* Too hot shortens component life and causes failures. Too cold risks condensation when equipment warms.
* ASHRAE's recommended data centre range is **18-27 °C** at the equipment air inlet.
* Use **hot aisle / cold aisle** layouts so exhaust air isn't drawn back into intakes.

### Humidity

<table><thead><tr><th width="160">Level</th><th>Risk</th></tr></thead><tbody><tr><td><strong>Too low</strong></td><td><mark style="color:$warning;"><strong>Static electricity</strong></mark>: electrostatic discharge can damage components.</td></tr><tr><td><strong>Too high</strong></td><td><mark style="color:$info;"><strong>Condensation and corrosion</strong></mark> of contacts and circuits.</td></tr></tbody></table>

Security texts commonly cite **40-60% relative humidity** as the target range. Anti-static flooring, wrist straps and grounding further reduce static risk.

### Airflow & Water

* **Positive pressurisation:** air flows **out** of the room when a door opens, so dust, smoke and contaminants are pushed away rather than drawn in.
* **Water detection:** sensors under raised floors and near cooling units, and no water pipes routed over equipment.
* **Dedicated HVAC** for server rooms, separate from general building HVAC, with an emergency shut-off.

***

## Fire Protection

### Fire Basics

Fire needs **heat, fuel and oxygen** (the fire triangle) plus a **chemical chain reaction** (the fire tetrahedron). Suppression works by removing one of these.

### Detection

<table><thead><tr><th width="200">Detector</th><th>How It Works</th></tr></thead><tbody><tr><td><strong>Smoke (ionisation)</strong></td><td>Responds quickly to small particles from fast, flaming fires.</td></tr><tr><td><strong>Smoke (photoelectric)</strong></td><td>Smoke scatters a light beam. Better at slow, smouldering fires.</td></tr><tr><td><strong>Heat (fixed temperature)</strong></td><td>Triggers at a set temperature. Fewer false alarms, slower response.</td></tr><tr><td><strong>Heat (rate-of-rise)</strong></td><td>Triggers when temperature climbs quickly.</td></tr><tr><td><strong>Flame</strong></td><td>Detects infrared or ultraviolet light from flames. Fastest, most expensive.</td></tr></tbody></table>

### Fire Classes

The **US** classes are what the SSCP tests. **UK/EU** classes differ, so don't mix them up.

<table><thead><tr><th width="220">Fuel</th><th width="120">US</th><th>UK / EU</th></tr></thead><tbody><tr><td>Ordinary combustibles (paper, wood)</td><td><strong>A</strong></td><td><strong>A</strong></td></tr><tr><td>Flammable liquids</td><td><strong>B</strong></td><td><strong>B</strong></td></tr><tr><td>Flammable gases</td><td>B</td><td><strong>C</strong></td></tr><tr><td>Electrical equipment</td><td><strong>C</strong></td><td>No class (electrical symbol)</td></tr><tr><td>Combustible metals</td><td><strong>D</strong></td><td><strong>D</strong></td></tr><tr><td>Cooking oils and fats</td><td><strong>K</strong></td><td><strong>F</strong></td></tr></tbody></table>

{% hint style="danger" %}
Never use water on an electrical fire while the equipment is live. Cut the power first, or use CO₂ or a clean agent.
{% endhint %}

### Suppression: Water-Based

<table><thead><tr><th width="160">System</th><th>How It Works</th><th>Use</th></tr></thead><tbody><tr><td><strong>Wet Pipe</strong></td><td>Pipes always full of water; heads open individually when heated.</td><td>Fastest and cheapest. Risk of leaks and freezing.</td></tr><tr><td><strong>Dry Pipe</strong></td><td>Pipes hold pressurised air; water enters only when heads open.</td><td>Unheated or freezing areas. Slower discharge.</td></tr><tr><td><strong>Pre-Action</strong></td><td>Pipes fill with water only after detection; heads still have to open individually.</td><td><mark style="color:$success;"><strong>Best water option for IT areas</strong></mark>: two triggers greatly reduce accidental discharge.</td></tr><tr><td><strong>Deluge</strong></td><td>Heads are always open; huge volume of water released at once.</td><td>High-hazard areas only. <strong>Not</strong> for IT.</td></tr></tbody></table>

### Suppression: Gas-Based

* **Clean agents** (e.g. FM-200 / HFC-227ea, Novec 1230) and **inert gases** (e.g. Inergen, argon) suppress fire without damaging equipment. Preferred for data centres.
* **CO₂** displaces oxygen and is **dangerous to people**. Use only in unoccupied areas, with pre-discharge alarms and delays.
* **Halon** was highly effective but damages the ozone layer. Production was banned under the Montreal Protocol, and it is no longer used in new systems.

***

## Emanation Security

Electronic equipment and copper cabling leak electromagnetic signals that can be captured and reconstructed from a distance.

* **TEMPEST:** the US government programme and standards for studying and limiting compromising emanations.
* **Faraday cage:** an enclosure (room, rack or bag) that blocks electromagnetic signals in both directions.
* **White noise:** broadcasting random noise to mask real emanations.
* **Control zones:** keeping a large enough physical distance, or shielded area, between sensitive equipment and anywhere an attacker could position receiving equipment.
* **Media choice:** fiber does not emit electromagnetic signals (see [Cabling](../networking/cabling.md)).
