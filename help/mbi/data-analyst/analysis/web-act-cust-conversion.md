---
title: Analyzing Website Activity and Customer Conversion Rates
description: Learn how to set up a dashboard that will track your website activity - including page views, sessions and users - as well as your customer conversion rate over time. 
---
# Analyzing Website Activity

MBI allows you to easily integrate your advertising cost data with the rest of your data. This not only enables you to understand your website activity, but empowers you to derive the percentage of visitors on your website that become a registered user or make a purchase.

In this article, we demonstrate how to set up a dashboard that will track your website activity - including page views, sessions and users - as well as your customer conversion rate over time.

## Prerequisites

**Import your advertising cost data** - Connect [Google AdWords](../importing-data/integrations/google-adwords.md) to MBI - this will automatically sync your AdWords spend in BI.

**Track user acquisition channel data** - In order to tie your Google AdWords data to specific orders in your database, we need to [track user acquisition](../analysis/google-track-user-acq.md) via Ecommerce in Google Analytics, allowing us to connect each order with a utm source and medium.

## User acquisition campaigns

This collection of reports is built using the following:

* Metrics that are automatically generated when you connect your Google AdWords data
* Basic metrics that should already be available on your account, like **Number of orders** and **New users**
* Dimensions created when joining your Google Ecommerce data to your database, like order's utm source and order's utm medium. Please contact our support team if these fields are not currently available in your account

## Building your reports

### A. Start by creating a report that shows the number of page views, sessions and users over time:

1. Create a new report.
1. Click **Add Metric**, then mouse over the _Google Analytics_ section at the bottom of the dropdown and select "Page Views".
1. Add another metric, again mousing over the _Google Analytics_ section, this time selecting "Sessions".
1. Add a third metric, again mousing over the _Google Analytics_ section, this time selecting "Users".
1. Now change your time period to a moving range, from 31 days ago to 1 day ago, and adjust the time interval to "by day".
1. Give your report a name (e.g., "Page views, sessions and users by day"), and click the green **Save**.

### B. Our second report will look at the number of page views over the past year:

1. Create a new report.
1. Click **Add Metric**, mouse over the _Google Analytics_ section at the bottom of the dropdown and select _Page Views_.
1. Change your time period to a moving range, from 13 months ago to 1 month ago, and adjust the time interval to _by month_.
1. Give your report a name, like "Page views by month," and click **Save**.

### C. The third chart will look at the bounce rate over the past year:

1. Create a new report.
1. Click **Add Metric**, mouse over the _Google Analytics_ section at the bottom of the dropdown and select _Bounce rate_.
1. Change your time period to a moving range, from 13 months ago to 1 month ago, and adjust the time interval to "by month".
1. Give your report a name, like _Bounce rate by month_, and click **Save**.

### D. Now, take a look at the average session length of new visitors compared to returning visitors:

1. Create a new report.
1. Click **Add Metric**, mouse over the _Google Analytics_ section at the bottom of the dropdown and select _Average Session Length_.
1. Change your time period to a moving range, from 13 months ago to 1 month ago, and adjust the time interval to _by month?
1. Add a _Group by_ and select _New or returning visitor_.  Check the _Show All_ box; then click **Apply**.
1. Give your report a name, like _Average session length_, and click **Save**.

### E. Next, take a look at your top referring domains in the last 30 days:

1. Create a new report.
1. Click **Add Metric**, mouse over the _Google Analytics_ section at the bottom of the dropdown and select _Sessions_.
1. Change your time period to a moving range, from 31 days ago to 1 day ago, and adjust the time interval to _none_.
1. Add a _Group by_ and select _ga:source_.  Check the _Show All_ box; then click **Apply**.
1. Add another _group by_ and select _ga:medium_. Again, check the _Show All_ box; then click **Apply**.
1. Give your report a name, like _Top 20 Referring Domains, 30 Days_, and click **Save**.

### F. Finally, take a look at conversion:

1. Create a new report.
1. Add the following metrics:

  * **New users**
    * Click **Hide** beneath the metric name

  * **Number of orders**
    * Add a filter for _Customer's order number_ = 1 and click **Apply**
    * Rename the metric by clicking on the metric name, calling it _Number of first orders;_ then click **Hide**

  * **Number of orders**
    * **Hide** the metric

  * **Users**
    * **Hide** the metric
    * Change the time period to _24 months ago to now_, and adjust time interval to _by month_
    * Add the following formulas by clicking **Formula**.
    * A/D then click **Apply**
    * Rename the formula _Registration conversion_
    * B/D then click **Apply**
    * Rename the formula _First order conversion_
    * C/D then click **Apply**
    * Rename the formula _Any order conversion_

  * Now give your report a name, like "Conversion by month," and then click **Save**

## Next steps

Now that you have access to data on your your web traffic and conversion rates, you can begin to mine this to drive business decisions. Which sites are best at driving traffic to your site?  Which of your campaigns are most effective at acquiring customers with the high lifetime value?

As you adjust ad spending and marketing strategy, you can continue to track the results in MBI, iterating on this dashboard to meet your company's evolving priorities.
