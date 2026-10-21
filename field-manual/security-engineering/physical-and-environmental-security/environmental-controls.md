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

# Environmental Controls

## Temperature

* Too hot shortens component life and causes failures. Too cold risks condensation when equipment warms.
* ASHRAE's recommended data centre range is **18-27 °C** at the equipment air inlet.
* Use **hot aisle / cold aisle** layouts so exhaust air isn't drawn back into intakes.

## Humidity

<table><thead><tr><th width="160">Level</th><th>Risk</th></tr></thead><tbody><tr><td><strong>Too low</strong></td><td><mark style="color:$warning;"><strong>Static electricity</strong></mark>: electrostatic discharge can damage components.</td></tr><tr><td><strong>Too high</strong></td><td><mark style="color:$info;"><strong>Condensation and corrosion</strong></mark> of contacts and circuits.</td></tr></tbody></table>

Security texts commonly cite **40-60% relative humidity** as the target range. Anti-static flooring, wrist straps and grounding further reduce static risk.

## Airflow & Water

* **Positive pressurisation:** air flows **out** of the room when a door opens, so dust, smoke and contaminants are pushed away rather than drawn in.
* **Water detection:** sensors under raised floors and near cooling units, and no water pipes routed over equipment.
* **Dedicated HVAC** for server rooms, separate from general building HVAC, with an emergency shut-off.
