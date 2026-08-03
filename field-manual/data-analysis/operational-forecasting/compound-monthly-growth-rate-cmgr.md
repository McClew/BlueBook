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

# Compound Monthly Growth Rate (CMGR)

Looking at the month-over-month (MoM) change of data points can be noisy. The CMGR smoothens the volatility to show us the "average" growth speed from one point in time to now. _The examples in this section all revolve around monthly calculations for MSP Tickets._

#### <i class="fa-chevron-up" style="color:$success;">:chevron-up:</i> <mark style="color:$success;">Positives</mark>

* <mark style="color:$success;">**Granular Visibility:**</mark> In fast-moving industries (like tech), waiting a year to see growth trends can be a death sentence. CMGR allows us to see how month-to-month changes impact long-term trajectory.
* <mark style="color:$success;">**Smooths Out Volatility:**</mark> Unlike simple average growth, CMGR accounts for the "compounding effect." It provides a steady, normalised rate that hides the "noise" of one anomalous month while still accurately representing the data.
* <mark style="color:$success;">**Ideal for Early-Stage Forecasting:**</mark> If you are a startup with 6 months of data, an annual rate (CAGR) is mostly guesswork. CMGR uses the actual, short-term data you have to project more realistic near-term targets.
* <mark style="color:$success;">**Benchmark for Burn Rate:**</mark> It helps businesses understand if their revenue growth is outpacing their monthly expenses (burn), which is vital for survival.

#### <i class="fa-chevron-down" style="color:$danger;">:chevron-down:</i> <mark style="color:$danger;">Negatives</mark>

* <mark style="color:$danger;">**Sensitivity to Outliers:**</mark> Because the timeframe is shorter, anomalous data can heavily distort the CMGR. These effects are only seen when the outlier is used as one of the data points.
* <mark style="color:$danger;">**Ignores Seasonality:**</mark> CMGR assumes a steady climb. If the data responds to seasonal effects, a CMGR calculated between these points in time can be highly inaccurate.
* <mark style="color:$danger;">**The "Compounding Trap":**</mark> The short-term view that CMGR provides can be highly misleading. This can lead to over, or under-optimism, and decisions that are not sustainable long-term.
* <mark style="color:$danger;">**Short-Term Focus:**</mark> It can encourage "growth at all costs" mentalities, leading teams to focus on quick wins to keep the monthly metric up rather than building sustainable, long-term value.

***

## The Formula

$$
\text{CMGR} = \left( \frac{\text{Latest Month Value}}{\text{First Month Value}} \right)^{\frac{1}{n-1}} - 1
$$

(Where $$n$$ is the number of months of data we have).

***

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

***

## Exponential Growth Modelling

When calculating Exponential Growth Modelling we can use a single formula to find a specific month in the future:

$$
\text{Future Value} = \text{Current Value} \times (1 + \text{CMGR})^\text{number of months}
$$
