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
---

# Risk Calculation

## Definitions

<i class="fa-computer" style="color:$info;">:computer:</i> <mark style="color:$info;">**Asset:**</mark> Anything of value to the organisation (data, servers, people, reputation).

<i class="fa-virus-covid" style="color:$warning;">:virus-covid:</i> <mark style="color:$warning;">**Vulnerability:**</mark> A weakness in the asset or its environment.

<i class="fa-user-ninja" style="color:$danger;">:user-ninja:</i> <mark style="color:$danger;">**Threat:**</mark> Any potential danger that could exploit the vulnerability.

<i class="fa-percent" style="color:$primary;">:percent:</i> <mark style="color:$primary;">**Risk:**</mark> The potential for loss or damage when a threat exploits a vulnerability.

***

## Qualitative Risk Calculations

The basic relationship is often expressed as: <mark style="color:$primary;">**Risk**</mark> = <mark style="color:$danger;">**Threat**</mark> × <mark style="color:$warning;">**Vulnerability**</mark>. Without a threat, a vulnerability is not a risk. Without a vulnerability, a threat is not a risk.

***

## Quantitative Risk Calculations

### Single Loss Expectancy (SLE)

The monetary loss expected from a single occurrence of a threat.

$$
SLE = AV * EF
$$

**SLE** = **Single Loss Expectancy**

**AV** = **Asset Value**

**EF** = **Exposure Factor**, is the percentage of the asset's value lost during a single incident

### Annualised Rate of Occurrence (ARO)

The estimated frequency of a threat occurring in a single year.

$$
Once \ every \ 10 \ years = 0.1 \ ARO
\\\\
Twice \ a \ year = 2.0 \ ARO
$$

### Annualised Loss Expectancy (ALE)

The total expected monetary loss from a specific risk over one year. This is the ultimate number we use to justify security spending.

$$
ALE = SLE * ARO
$$

**ALE** = **Annualised Loss Expectancy**

**SLE** = **Single Loss Expectancy**

**ARO** = **Annualised Rate of Occurrence**
