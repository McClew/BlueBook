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

# Predicting Time Spent (Efficiency vs. Volume)

In this example we are calculating the time spent on a ticket based on its 'Issue Type'.

We need to find the Average Handle Time (AHT) for each 'Issue Type' to see if we are getting faster or if the complexity is rising.

***

## Calculate AHT

$$\text{Total Time for Issue Type} \div \text{Volume of Issue Type}$$.

***

## Identify the "Time Sinks"

Compare the AHT of "Phishing" vs. "Firewall Config."

***

## The Projection

If "Phishing" tickets are growing at 20% MoM, but the AHT is also increasing (perhaps due to more sophisticated attacks), your staffing needs will hit a breaking point much faster than ticket counts alone suggest.
