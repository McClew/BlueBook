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

# Compound Monthly Growth Rate (CMGR)

Looking at the month-over-month (MoM) change of data points can be noisy. The CMGR smoothens the volatility to show us the "average" growth speed from one point in time to now. _The examples in this section all revolve around monthly calculations for MSP Tickets._

## The Formula

$$
\text{CMGR} = \left( \frac{\text{Latest Month Value}}{\text{First Month Value}} \right)^{\frac{1}{n-1}} - 1
$$

(Where $$n$$ is the number of months of data we have).

## How to use it

1. Divide the most recent ticket count by the point in time required (e.g., divide Decembers ticket count by Januarys count).
2. Apply the exponent (if we have 12 months of data, use $$1/11$$).
3. Subtract 1 to get the percentage. For example, if the final result was 0.08303527598... this would be 8.3%.

{% hint style="info" %}
#### Why this helps

If our CMGR is 12%, we can estimate next month by multiplying this month's total by the formulas result.
{% endhint %}

### Calculating the Exponent

$$
\frac{1}{n-1}
$$

$$n$$ is the total number of months for which we have data. The "-1" is used because we are measuring the intervals between the months, not the months themselves.

Using the January to December example ($$n=12$$):

1. Find the denominator: $$12 - 1 = 11$$.
2. Calculate the fraction: $$1 \div 11 \approx 0.09\dot{0}\dot{9}$$.
3. Apply to the formula: We will raise the result to the power of 0.0909.

## Exponential Growth Modelling

When calculating
