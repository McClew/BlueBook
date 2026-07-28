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

<i class="fa-computer" style="color:$success;">:computer:</i> <mark style="color:green;">**Asset:**</mark> Anything of value to the organisation (data, servers, people, reputation).

<i class="fa-virus-covid" style="color:$warning;">:virus-covid:</i> <mark style="color:$warning;">**Vulnerability:**</mark> A weakness in the asset or its environment.

<i class="fa-user-ninja" style="color:$danger;">:user-ninja:</i> <mark style="color:$danger;">**Threat:**</mark> Any potential danger that could exploit the vulnerability.

<i class="fa-percent" style="color:$primary;">:percent:</i> <mark style="color:$primary;">**Risk:**</mark> The potential for loss or damage when a threat exploits a vulnerability.

***

## Qualitative Risk Calculations

Qualitative risk analysis evaluates risk based on subjective measures rather than objective financial data. Instead of calculating dollars and exact percentages, use experience, intuition, best practices, and expert judgment to categorise risks.

Evaluate two primary factors:

1. <mark style="color:$info;">**Likelihood (Probability):**</mark> How likely is this threat to occur? (e.g., <mark style="color:$success;">Rare</mark>, <mark style="color:$warning;">Possible</mark>, <mark style="color:$danger;">Certain</mark>).
2. <mark style="color:$info;">**Impact (Consequence):**</mark> If the threat occurs, how bad will the damage be to the organisation? (e.g., <mark style="color:$success;">Minor</mark>, <mark style="color:$warning;">Moderate</mark>, <mark style="color:$danger;">Severe</mark>).

The basic relationship is often expressed as: <mark style="color:$primary;">**Risk**</mark> = <mark style="color:$danger;">**Threat**</mark> × <mark style="color:$warning;">**Vulnerability**</mark>. Without a threat, a vulnerability is not a risk. Without a vulnerability, a threat is not a risk.

#### <i class="fa-chevron-up" style="color:$success;">:chevron-up:</i> <mark style="color:$success;">Pros:</mark>

* <mark style="color:$success;">**Fast and easy to perform:**</mark> We don't need months of historical data or financial modeling to categorise a risk as "High."
* <mark style="color:$success;">**Easy to communicate:**</mark> Management readily understands color-coded matrices (Red = Bad, Green = Good).
* <mark style="color:$success;">**Great for initial triage:**</mark> It quickly helps us prioritise which risks need deeper (often quantitative) analysis.

#### <i class="fa-chevron-down" style="color:$danger;">:chevron-down:</i> <mark style="color:$danger;">The Cons:</mark>

* <mark style="color:$danger;">**Highly subjective:**</mark> Our definition of a "High" impact might differ completely from a colleague's definition.
* <mark style="color:$danger;">**Cannot justify specific spending:**</mark> We cannot perform a true cost-benefit analysis and can't confidently spend £10,000 to mitigate a risk simply categorised as "Red."

### The Risk Matrix

The most common tool for qualitative analysis is the Risk Matrix (also called a Risk Heat Map). It visually plots _Likelihood_ against _Impact_ to determine the overall Risk Level. Organisations often use a 3x3, 4x4, or 5x5 grid.

#### 3x3 Example

| <p><strong>Likelihood ➡</strong><br><strong>Impact ⬇</strong></p> | <mark style="color:blue;">**Low (1)**</mark>       | <mark style="color:yellow;">**Medium (2)**</mark>  | <mark style="color:red;">**High (3)**</mark>       |
| ------------------------------------------------------------------ | -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| <mark style="color:red;">**High (3)**</mark>                       | <mark style="color:yellow;">Medium Risk (3)</mark> | <mark style="color:orange;">High Risk (6)</mark>   | <mark style="color:red;">Critical Risk (9)</mark>  |
| <mark style="color:yellow;">**Medium (2)**</mark>                  | <mark style="color:green;">Low Risk (2)</mark>     | <mark style="color:yellow;">Medium Risk (4)</mark> | <mark style="color:orange;">High Risk (6)</mark>   |
| <mark style="color:blue;">**Low (1)**</mark>                       | <mark style="color:blue;">Very Low Risk (1)</mark> | <mark style="color:green;">Low Risk (2)</mark>     | <mark style="color:yellow;">Medium Risk (3)</mark> |

By finding where a specific threat's _Likelihood_ and _Impact_ intersect, we get a clear, immediate prioritisation category. A critical server facing a highly likely threat (<mark style="color:$danger;">Critical Risk - 9</mark>) gets attention before a minor system facing a rare threat (<mark style="color:blue;">Very Low Risk - 1</mark>).

***

## Quantitative Risk Calculations

While qualitative analysis relies on human judgment and color-coded matrices, quantitative analysis uses numerical values to measure risk. It removes the subjectivity and replaces it with hard data, historical trends, and financial modeling.

#### <i class="fa-chevron-up" style="color:$success;">:chevron-up:</i> <mark style="color:$success;">Pros:</mark>

* <mark style="color:$success;">**Objective and Precise:**</mark> It relies on verifiable data and financial metrics rather than subjective opinions.
* <mark style="color:$success;">**Cost-Benefit Analysis:**</mark> Because it gives us a definitive "dollar" amount (ALE), it allows you to clearly justify the budget for specific security controls, like purchasing a firewall or a redundant hard drive array.
* <mark style="color:$success;">**Clear ROI:**</mark> We can mathematically prove whether a security countermeasure saves the company money over time.

#### <i class="fa-chevron-down" style="color:$danger;">:chevron-down:</i> <mark style="color:$danger;">The Cons:</mark>

* <mark style="color:$danger;">**Time-Consuming & Complex:**</mark> It requires complex financial modeling and significant time to perform.
* <mark style="color:$danger;">**Relies on Historical Data:**</mark> If we do not have accurate historical data or metrics, we cannot accurately calculate the ARO or the EF, making the entire calculation unreliable.
* <mark style="color:$danger;">**Hard to Quantify Intangibles:**</mark> It is very difficult to assign a strict "dollar" values to things like "brand reputation" or "customer trust."

{% hint style="info" %}
#### Hard to Quantify Intangibles

While it can be very difficult to assign specific financial values to more ethereal data such as brand reputation, it is important to note: _<mark style="color:$primary;">these values can always be calculated</mark>_.
{% endhint %}

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
