---
title: Building a dashboard for investors
description: Learn how to build a dashboard for investors. 
---
# Build Investor Dashboard

Many of our clients are working with investors and need to share information from platform with them, but the dashboards that you create to make day-to-day business decisions may not be what an investor is looking for. Here we cover some best practices for how to create a dashboard that is comprehensive but simple, ideal for sharing with active and potential investors.

Here is what you need to create reports for your investor dashboard:

## Scalar Reports

* **All-time revenue**
* **Distinct buyers**
* **All-time number of orders**
* **AOV**
* **Items sold**

## Visual Reports

* **Revenue by quarter**
    * Metric – Revenue
* **Revenue from 1st time orders vs repeat orders**
    * Metric – First time order revenue
    * Filter – User's order number is equal to 1
  * Metric 2 – Repeat order revenue
    * Filter – User's order number is greater than 1
  * Uncheck the box for Multiple Y-Axes
  * Change to a Stacked Column chart
* **AOV by quarter**
  * Metric 1 – Revenue
    * Hide this metric
  * Metric 2 – Number of orders
    * Hide this metric
  * Formula – AOV
    * A/B
* **All-time revenue by source**
  * Metric – Revenue
  * Group by customer's utm_source
* **Revenue from top 10 products**
  * Metric – Product revenue
    * Hide the chart
    * Group by Product's name. Select all products.
    * Set the time range to All-Time
    * Set the time interval to None
    * In "Show top/bottom", show only the top 10 sorted by Product profit
* **Cumulative distinct buyers by quarter**
  * Metric – Distinct buyers
    * Perspective – Cumulative
* **Site visits - New vs. repeat by month**
* Sessions

With a **Google Analytics** integration, you can include reports on:

* Site visits
* Conversion rate

With [Magento's Data Enrichment services](https://magento.com/services), you can include reports on:

* Unique customers by state/region, age, gender, etc.

## Other Tips

* Use a clear and concise [naming convention](../../best-practices/naming-elements.md)
* Share the dashboard with investor users
* Or send it via [Automated email summary](../../data-user/export-data/email-summaries.md)
* Create only one dashboard. This will make the content easier to maintain, and you will know exactly what your investors are looking at.

Organize your reports thoughtfully and pay attention to detail. Once complete, the dashboard will look similar to:

![](../../mbi/assets//mceclip0.png)
