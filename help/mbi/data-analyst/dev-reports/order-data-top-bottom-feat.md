---
title: Order data using the Show Top/Bottom feature
description: Learn how to order your data using the Show Top/Bottom feature.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
---
# Ordering Data using `Show Top/Bottom` feature

You can do more in the `Visual Report Builder` than create analyses that trend over time. For example, you can build a report to show how valuable your acquisition and marketing channels are, but you can also build a report that shows only the top five performers. Similarly, you can refocus your marketing efforts by creating a report that shows you which states generate the most revenue.

This kind of sorting and ordering of data can be done in reports that use both a `Group By` and a `Time Interval of None`. When both of these elements are in a report, the `Show Top/Bottom` feature displays above the chart preview. This feature allows you to see the top (highest to lowest) and bottom (lowest to highest) data points based on the parameters you set.

![Show Top/Bottom feature in the Visual Report Builder.](../../assets/Show_Top_Bottom.png)

## How do I use this? {#how}

Click the **[!UICONTROL Show Top/Bottom link]** to set the display and sorting parameters. The number in the textbox can either be a whole number (like `5`) or `ALL`. Next, you can choose to sort the report either by the metric OR by the grouping.

For example, if you wanted to display the five referral sources that brought in the most revenue, this is how you do it:

1. Add the `Revenue` metric to the report.

1. Add a `Group By` to segment the metric by referral source.

1. Set `Time Interval` to `None`.

1. In the `Show Top/Bottom` settings, set the display to `5` so only the referral sources with the top five total revenue amounts are included in the report.

>[!NOTE]
>
>Because the report does not have a `Time Interval`, the values - in this case, the top five referral sources - can change over time. If one referral source surpasses another in terms of revenue, the order in which the sources display changes.

## What about using multiple metrics? {#multiplemetrics}

Using this feature gets complicated when tHere is more than one metric in a report because each metric can only be sorted by itself or by one of the groupings.

Say you built a report with both the `Revenue` and `Number of orders` metrics, grouped by referral source. `Revenue` can only be sorted by `Revenue` or referral source and `Number of orders` can only be sorted by `Number of orders` or referral source.

This means that while you can show the `Revenue` from only the top `5` revenue-generating referral sources, you cannot show the number of orders also by the top `5` revenue-generating referral sources. Simply put: when there are multiple metrics, the best bet is to sort each metric by the grouping.

Below is an example of a chart that sorted the `Revenue` metric by itself instead of by the grouping. As you can see, not sorting the metric by the grouping created a strange (and ultimately unhelpful) report:

![Strange and unhelpful report results.](../../assets/strange-report-results.png)

If you had sorted both metrics by the grouping, the chart would look like this:

![Sorting both metrics by the grouping.](../../assets/sort-metrics-by-grouping.png)

## How are values sorted by default? {#defaultsorting}

When only one metric is included in a report with a `Group by` and a `Time Interval` of `None`, the default ordering in the `Visual Report Builder` is to show the top values based on the metric. In this instance, the `Show Top/Bottom` feature may not be necessary if this serves your needs.

This example looks at how many opportunities that your sales reps have closed. This table is automatically sorted from highest to lowest based on the metric, in this case `Won Opportunities`.

![Ordering by the metric.](../../assets/Ordered_by_metric.png)

However, when a second metric is added, the default is to order the top based on the grouping. As metrics and groupings are added, the default sorting is based on the first grouping, then the second grouping, and so on.

![Ordering by the grouping.](../../assets/Ordered_by_grouping.png)

## Wrapping up {#wrapup}

While some basic features are covered here, this feature has many interesting uses.

Think about the previous sales rep and opportunities example. Removing the `Time Interval`, applying a `Group By`, and sorting the data based on the grouping allowed us to get a detailed picture of each rep's number of won opportunities. Also, using the `Show Top/Bottom` feature let us discover who the top performers are.
