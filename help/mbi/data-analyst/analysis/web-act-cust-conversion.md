---
title: Analyzing Website Activity and Customer Conversion Rates
description: Learn how to set up a dashboard that will track your website activity - including page views, sessions and users - as well as your customer conversion rate over time.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
---
# Analyzing Website Activity

[!DNL MBI] allows you to easily integrate your advertising cost data with the rest of your data. This not only enables you to understand your website activity, but empowers you to derive the percentage of visitors on your website that become a registered user or make a purchase.

In this article, we demonstrate how to set up a dashboard that will track your website activity - including page views, sessions and users - as well as your customer conversion rate over time.

## Prerequisites

**Import your advertising cost data** - Connect [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) to [!DNL MBI] - this will automatically sync your [!DNL AdWords] spend in BI.

**Track user acquisition channel data** - To tie your [!DNL Google AdWords] data to specific orders in your database, we need to [track user acquisition](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce], allowing us to connect each order with a utm source and medium.

## User acquisition campaigns

This collection of reports is built using the following:

* Metrics that are automatically generated when you connect your [!DNL Google AdWords] data
* Basic metrics that should already be available on your account, like `Number of orders` and `New users`
* Dimensions created when joining your [!DNL Google Analytics Ecommerce] data to your database, like order's utm source and order's utm medium. Contact our support team if these fields are not currently available in your account

## Building your reports

**Start by creating a report that shows the number of page views, sessions and users over time:**

1. Create a new report.
1. Click **[!UICONTROL Add Metric]**, then mouse over the [!DNL Google Analytics] section at the bottom of the dropdown and select `Page Views`.
1. Add another metric, again mousing over the [!DNL Google Analytics] section, this time selecting `Sessions`.
1. Add a third metric, again mousing over the [!DNL Google Analytics] section, this time selecting `Users`.
1. Now change your time period to a moving range, from 31 days ago to 1 day ago, and adjust the time interval to `by day`.
1. Give your report a name (for example, `Page views, sessions and users by day`), and click **[!UICONTROL Save]**.

**Our second report will look at the number of page views over the past year:**

1. Create a new report.
1. Click **[!UICONTROL Add Metric]**, mouse over the [!DNL Google Analytics] section at the bottom of the dropdown and select _Page Views_.
1. Change your time period to a moving range, from 13 months ago to 1 month ago, and adjust the time interval to `by month`.
1. Give your report a name, like `Page views by month,` and Click **[!UICONTROL Save]**.

**The third chart will look at the bounce rate over the past year:**

1. Create a new report.
1. Click **[!UICONTROL Add Metric]**, mouse over the [!DNL Google Analytics] section at the bottom of the dropdown and select _Bounce rate_.
1. Change your time period to a moving range, from 13 months ago to 1 month ago, and adjust the time interval to `by month`.
1. Give your report a name, like `Bounce rate by month`, and Click **[!UICONTROL Save]**.

**Now, take a look at the average session length of new visitors compared to returning visitors:**

1. Create a new report.
1. Click **UICONTROL Add Metric**, mouse over the [!DNL Google Analytics] section at the bottom of the dropdown and select `Average Session Length`.
1. Change your time period to a moving range, from 13 months ago to 1 month ago, and adjust the time interval to `by month`?
1. Add a `Group by` and select `New or returning visitor`.  Check the `Show All` box; then click **[!UICONTROL Apply]**.
1. Give your report a name, like `Average session length`, and Click **[!UICONTROL Save]**.

**Next, take a look at your top referring domains in the last 30 days:**

1. Create a new report.
1. Click **[!UICONTROL Add Metric]**, mouse over the [!DNL Google Analytics] section at the bottom of the dropdown and select `Sessions`.
1. Change your time period to a moving range, from 31 days ago to 1 day ago, and adjust the time interval to `none`.
1. Add a `Group by` and select `ga:source`.  Check the _Show All_ box; then click **[!UICONTROL Apply]**.
1. Add another `group by` and select `ga:medium`. Again, check the `Show All` box; then click **[!UICONTROL Apply]**.
1. Give your report a name, like `Top 20 Referring Domains, 30 Days`, and click **[!UICONTROL Save]**.

**Finally, take a look at conversion:**

1. Create a new report.
1. Add the following metrics:

* `New users`
    * Click **[!UICONTROL Hide]** beneath the metric name

* `Number of orders`
    * Add a filter for `Customer's order number` = 1 and click **[!UICONTROL Apply]**
    * Rename the metric by clicking on the metric name, calling it `Number of first orders`,then click **[!UICONTROL Hide]**

* `Number of orders`
    * **[!UICONTROL Hide]** the metric

* `Users`
    * **[!UICONTROL Hide]** the metric
    * Change the time period to `24 months ago to now`, and adjust time interval to `by month`.
    * Add the following formulas by clicking **[!UICONTROL Formula]**.
    * A/D then click **[!UICONTROL Apply]**
    * Rename the formula `Registration conversion`
    * B/D then click **[!UICONTROL Apply]**
    * Rename the formula `First order conversion`
    * C/D then click **[!UICONTROL Apply]**
    * Rename the formula `Any order conversion`

* Now give your report a name, like `Conversion by month`, and then click **[!UICONTROL Save]**.

## Next steps

Now that you have access to data on your your web traffic and conversion rates, you can begin to mine this to drive business decisions. Which sites are best at driving traffic to your site?  Which of your campaigns are most effective at acquiring customers with the high lifetime value?

As you adjust ad spending and marketing strategy, you can continue to track the results in [!DNL MBI], iterating on this dashboard to meet your company's evolving priorities.
