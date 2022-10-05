---
title: Cohort Report Builder for Non-Date Based Cohorts
description: Learn to group users by a similar activity or attribute.
---
# Cohort Report Builder for Non-Date-Based Cohorts

Our [Cohort Report Builder](../dev-reports/cohort-rpt-bldr.md) has been great at helping merchants study how different subsets of users behave over time. In the past, the Cohort Report Builder was mainly optimized for grouping users by a common **cohort date** (i.e., the set of all customers who made their first purchase in a given month). The Non-Date Based Cohort feature now gives you the power to group users by a similar activity or attribute. Take a look at a few use cases for this feature.

## Use Cases

This is not a comprehensive list, but here are some potential analyses that can be accomplished with this feature:

* Examining the revenue of customers acquired from Google vs. Facebook
* Analyzing customers whose first purchase was made in the US vs. Canada
* Looking at the behavior of customers acquired from various ad campaigns

## How to Create Your Analysis

1. Click **Report Builder** on the left tab or **Add Report** > **Create Report** in any dashboard.

1. In the Report Builder selection screen, click **Create Report** next to the **Visual Report Builder** option.

### Adding a metric

Now that we are in the Report Builder, we add the metric that we want to perform the analysis on (example: **Revenue** or **Orders**).

>[!NOTE]
>
>Native Google Analytics metrics are not compatible with the Cohort Report Builder.** Our goal for this example is to look at revenue over time for first-order customers who were acquired through different GA sources.

### Toggle Metric View to Cohort

![1-toggle metric view to cohort](../../mbi/assets/1-toggle-metric-view-to-cohort.png)<!--{: width="300" height="318"}-->

This opens up a new window where we can configure the details of the Cohort Report.

Five specifications are needed to build a Cohort report:

1. How to group the cohorts
1. Selecting cohorts
1. Action timestamp
1. Cohort first action time range
1. Time range after cohort occurrence

![cohort-groups](../../mbi/assets/2-cohort-groups.png)<!--{: width="300" height="336"}-->

![cohort-first-action-time-range](../../mbi/assets/3-cohort-first-action-time-range.png)<!--{: width="400" height="554"}-->

#### 1. Grouping cohorts

Cohorts are grouped together by a behavior characteristic, in this example "Customer's first order GA source". Note that the options available here are columns that are already designated as **groupable** for the metric.

#### 2. Selecting cohorts

You have the option to show all results for the given characteristic. Since this can result in a large number of cohorts, you can select the specific cohorts (which will correspond to the various values available for "Customer's first order GA source") that you need.

![cohort-groups](../../mbi/assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. Action timestamp

This will allow you to choose a date-based column other than the column on which the metric is created. Below, we'll look at selecting the time range that applies to the given action timestamp.

#### 4. Cohort first action time range

Here is where you will select the date range that contains the cohorts action timestamp (so, customers who had the first order from November 2017 to October 2018). This can be a moving date range or a fixed date range.

#### 5. Time range after cohort occurrence

Do you want to see the cohorts over time by month, week, or year? Here is where you will make those selections. Beneath that section, you will select the time range after the cohort action timestamp occurred. For example, this will show you twelve months of data for the customers who placed the first order during the action time range.

![cohort-first-action-time-range](../../mbi/assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

### Other notes

* Filters applied to your metrics will remain intact when you toggle between Standard and Cohort views
* For more details on Perspectives, you can go to [this article](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
