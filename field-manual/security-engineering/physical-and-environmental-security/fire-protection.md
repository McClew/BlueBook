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

# Fire Protection

## Fire Basics

Fire needs **heat, fuel and oxygen** (the fire triangle) plus a **chemical chain reaction** (the fire tetrahedron). Suppression works by removing one of these.

## Detection

<table><thead><tr><th width="200">Detector</th><th>How It Works</th></tr></thead><tbody><tr><td><strong>Smoke (ionisation)</strong></td><td>Responds quickly to small particles from fast, flaming fires.</td></tr><tr><td><strong>Smoke (photoelectric)</strong></td><td>Smoke scatters a light beam. Better at slow, smouldering fires.</td></tr><tr><td><strong>Heat (fixed temperature)</strong></td><td>Triggers at a set temperature. Fewer false alarms, slower response.</td></tr><tr><td><strong>Heat (rate-of-rise)</strong></td><td>Triggers when temperature climbs quickly.</td></tr><tr><td><strong>Flame</strong></td><td>Detects infrared or ultraviolet light from flames. Fastest, most expensive.</td></tr></tbody></table>

## Fire Classes

The **US** classes are what the SSCP tests. **UK/EU** classes differ, so don't mix them up.

<table><thead><tr><th width="220">Fuel</th><th width="120">US</th><th>UK / EU</th></tr></thead><tbody><tr><td>Ordinary combustibles (paper, wood)</td><td><strong>A</strong></td><td><strong>A</strong></td></tr><tr><td>Flammable liquids</td><td><strong>B</strong></td><td><strong>B</strong></td></tr><tr><td>Flammable gases</td><td>B</td><td><strong>C</strong></td></tr><tr><td>Electrical equipment</td><td><strong>C</strong></td><td>No class (electrical symbol)</td></tr><tr><td>Combustible metals</td><td><strong>D</strong></td><td><strong>D</strong></td></tr><tr><td>Cooking oils and fats</td><td><strong>K</strong></td><td><strong>F</strong></td></tr></tbody></table>

{% hint style="danger" %}
Never use water on an electrical fire while the equipment is live. Cut the power first, or use CO₂ or a clean agent.
{% endhint %}

## Suppression: Water-Based

<table><thead><tr><th width="160">System</th><th>How It Works</th><th>Use</th></tr></thead><tbody><tr><td><strong>Wet Pipe</strong></td><td>Pipes always full of water; heads open individually when heated.</td><td>Fastest and cheapest. Risk of leaks and freezing.</td></tr><tr><td><strong>Dry Pipe</strong></td><td>Pipes hold pressurised air; water enters only when heads open.</td><td>Unheated or freezing areas. Slower discharge.</td></tr><tr><td><strong>Pre-Action</strong></td><td>Pipes fill with water only after detection; heads still have to open individually.</td><td><mark style="color:$success;"><strong>Best water option for IT areas</strong></mark>: two triggers greatly reduce accidental discharge.</td></tr><tr><td><strong>Deluge</strong></td><td>Heads are always open; huge volume of water released at once.</td><td>High-hazard areas only. <strong>Not</strong> for IT.</td></tr></tbody></table>

## Suppression: Gas-Based

* **Clean agents** (e.g. FM-200 / HFC-227ea, Novec 1230) and **inert gases** (e.g. Inergen, argon) suppress fire without damaging equipment. Preferred for data centres.
* **CO₂** displaces oxygen and is **dangerous to people**. Use only in unoccupied areas, with pre-discharge alarms and delays.
* **Halon** was highly effective but damages the ozone layer. Production was banned under the Montreal Protocol, and it is no longer used in new systems.
