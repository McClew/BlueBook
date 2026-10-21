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

# Power Protection

<table><thead><tr><th width="200">Control</th><th>Protects Against</th><th>Notes</th></tr></thead><tbody><tr><td><strong>Surge Protector</strong></td><td>Spikes, surges</td><td>Diverts excess voltage. Does nothing for low voltage or loss of power.</td></tr><tr><td><strong>Line / Power Conditioner</strong></td><td>Noise, sags, surges</td><td>Smooths and regulates the supply. No battery, so no protection from outages.</td></tr><tr><td><strong>UPS</strong></td><td>Short outages, sags, brownouts</td><td>Battery bridge long enough to shut down cleanly or for a generator to start.</td></tr><tr><td><strong>Generator</strong></td><td>Prolonged outages</td><td>Needs fuel supply, regular load testing and a UPS to cover its start-up time.</td></tr><tr><td><strong>Redundant Supply</strong></td><td>Single-point failures</td><td>Dual power supplies in devices, dual PDUs, and ideally dual feeds from separate substations.</td></tr></tbody></table>

## Power Anomalies

<table><thead><tr><th width="227">Condition</th><th width="259">Momentary</th><th>Prolonged</th></tr></thead><tbody><tr><td><strong>High voltage</strong></td><td><mark style="color:$warning;"><strong>Spike</strong></mark></td><td><mark style="color:$warning;"><strong>Surge</strong></mark></td></tr><tr><td><strong>Low voltage</strong></td><td><mark style="color:$info;"><strong>Sag / Dip</strong></mark></td><td><mark style="color:$info;"><strong>Brownout</strong></mark></td></tr><tr><td><strong>Loss of power</strong></td><td><mark style="color:$danger;"><strong>Fault</strong></mark></td><td><mark style="color:$danger;"><strong>Blackout</strong></mark></td></tr></tbody></table>

## Terminology

* <mark style="color:$info;">**Inrush current:**</mark> the initial surge drawn when equipment is switched on. Powering up many devices at once can trip breakers or cause a sag for everything else on the circuit.
* <mark style="color:$info;">**Noise:**</mark> EMI or RFI interference carried on the power line (transient noise), often from motors, fluorescent lighting or other equipment sharing the circuit.

## UPS Types

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
