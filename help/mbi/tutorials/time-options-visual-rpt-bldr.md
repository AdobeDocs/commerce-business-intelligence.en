---
title: Use Time Options in the Visual Report Builder
description: Learn to analyze the data in your report for a specific time period.
---
# Use `Time` Options in `Visual Report Builder`

One of the features of the `Visual Report Builder` is the global `Time Range` and `Interval` settings. These settings allow you to analyze the data in your report for a specific time period.

However, for some analyses, you may need to consider different Time Ranges or Time Intervals in the same report. That is where `Time` Options come in. To give you a better idea of how to use `Time` Options in your reports, this tutorial will cover the following use cases:

* [Analyzing Metrics without Timestamps](#notimestamp)
* [Giving One Metric an Independent Time Interval](#independenttimeinterval)
* [Comparing the Same Metric Across Different Time Ranges](#difftimerange)

If you want to follow along with some of the sample reports discussed in this topic, open the [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) before continuing.

## Analyzing Metrics without Timestamps {#notimestamp}

Some metrics simply cannot trend over time because the data is not collected or stored with an associated timestamp. For example, an inventory table will often contain only one row for each SKU. In that case, you should [create the metric](../data-user/reports/ess-manage-data-metrics.md) without specifying a timestamp.

When using such a metric in your reporting, you notice that adding this metric to a report automatically sets an independent `Time Interval` of `None` and `Time Range` of `Global`:

![](../assets/Metrics_without_timestamps.gif)

## Giving One Metric an Independent Time Interval {#independenttimeinterval}

`Time` Options allow you to create time-based 100% charts to identify which day, week, month, or year contributed the most value during a specific time range. In this section, we create a chart that shows you the percent of revenue generated in each calendar month of a year.

This type of report can be useful if you want to compare revenue generated year-over-year. For example, if a chart for 2015 revealed that January contributed 18% of revenue for the year and one for 2016 showed only 8%, you could start researching what might have happened.

1. Add your `Revenue` metric to the report.
1. Click **[!UICONTROL Duplicate]** to make a copy of the metric.
1. Click the global **[!UICONTROL Time Range]** option, then **[!UICONTROL Moving Time Range]**. Set this to `Last Year`.
1. Click the global **[!UICONTROL Time Interval]** option and set it to `Monthly`.
1. Report Builder automatically adds a second Y-axis for a second metric. Deselect the `Multiple Y-Axes` box.
1. Next, we apply an independent `Time Interval` to the first metric. Click **[!UICONTROL Time Options]** (clock icon) to the right of the `first Revenue metric`.
1. Click **[!UICONTROL Time Options]** in the expanded window that displays above the report.
1. In the dropdown, set the following:

   * `Time Interval`: set this to `None`.

   * `Time Range`: set this to `Last Year` by first clicking **[!UICONTROL Custom]**, then **[!UICONTROL Moving Range]**, and finally selecting the `Last Year` option.

   * Click **[!UICONTROL Apply]** to save the interval and range settings. This creates a metric that calculates the total revenue for the previous year. Next, we use this metric as the denominator in a formula.

   * To see the percent of revenue for each month, we need to add a formula to the report. Click **[!UICONTROL Add Formula]**.

   * Enter `B/A` in the formula field and select `% Percent` from the dropdown next to the text field. This formula divides the amount of revenue from a specific month last year by the total amount of revenue last year.

   * Click **[!UICONTROL Apply Changes]**.

   * Hide both of your input metrics and rename the formula.

Now we can see just how impactful each month was last year:

![](../assets/Independent_Time_Int.png)

## Comparing the Same Metric Across Different Time Ranges {#difftimerange}

This example uses a custom dimension called `Day number of the month`. If you want to create this report and do not already have this dimension in your Data Warehouse, [contact support](../guide-overview.md) for assistance.

The two most common examples in this category are (1) comparing growth metrics (revenue year-over-year, month-over-month, etc.) and (2) better understanding recent inventory or item sales trends.

To demonstrate this use case, we look at the daily revenue for the previous month compared to the same month from the previous year. Let's say we want to look at the revenue for each day of January 2016 and then compare that to January 2015, January 2014, and so on – this report would show us that.

1. Add your `Revenue` metric to the report.
1. Click **[!UICONTROL Duplicate]** to make a copy of the metric.
1. Rename the first metric to `Items sold last 7 days` and the second metric to `Items sold last 28 days`.
1. Click **[!UICONTROL Time Range]**, then **[!UICONTROL Moving Time Range]**. Set this to `Last Month`.
1. Click **[!UICONTROL Time Interval]** and set it to `None`.
1. Click **[!UICONTROL Time Options]** (clock icon) next to the second `Revenue` metric.
1. Click **[!UICONTROL Time Options]** in the expanded window that displays above the report.
1. In the dropdown, set the following:

   * `Time Interval`: set this to `None`.

   * `Time Range`: set this to `From 14 Months Ago To 13 Months Ago` by first clicking **[!UICONTROL Custom]** then **[!UICONTROL Moving Range]**. Use the fields and dropdowns at the top of the menu to set the range. This setting allows us to see the revenue for the previous month, but in the previous year.

   Do not worry if the metric disappears from the report - setting an independent time options automatically hides the metric from the report. To redisplay it, click **[!UICONTROL Show]** next to the metric.

   ![](../assets/Different_Time_Ranges.gif)

   * Click **[!UICONTROL Apply]** to save the interval and range settings.

   * Next, we add our custom `Day number of the month` dimension by clicking **[!UICONTROL Group By]** and selecting the dimension. This will return the day number of the month of an order - for example, an order placed on March 2 will return `2`.

   * In the `Group By` dropdown, select `Show All` and click **[!UICONTROL Apply]**. This will effectively create the X-axis values for the report:

   ![](../assets/TO4.png)

   * Rename the metrics. In our example, the first metric is `Revenue - 2015` and the second is `Revenue - 2014`.

Another common use of custom `Time Options` is to determine weeks of supply. Especially during the holiday season or a special promotional period, you may want to consider items sold over the last week, month, and previous promotional period to make informed purchasing decisions.

Remember to set the time ranges to what you need when building this report yourself.

1. Add your `Items Sold` metric to the report.
1. Click **[!UICONTROL Duplicate]** to make a copy of the metric.
1. Rename the metrics. You can use the same names we are, or use something that is similar:
   1. Rename the first metric to `Items sold last 7 days`.
   1. Rename the second metric to `Items sold last 28 days`.
1. On the `Items sold last 7 days` metric, click the global **[!UICONTROL Time Range]** option then **[!UICONTROL Moving Time Range]**. For this example, we set it to `Last 7 Days`.
1. Click **[!UICONTROL Time Interval]** and set it to `None`.
1. Next, we define the `Time Options` for the `Items sold last 28 days` metric. Click **[!UICONTROL Time Options]** (clock icon) to the right of the `second Items sold` metric.
1. Click **[!UICONTROL Time Options]** in the expanded window that displays above the report.
1. In the dropdown, set the following:

   * `Time Interval`: set this to `None`.
   * `Time Range`: set this to `From 29 days to 1 day ago` by first clicking **[!UICONTROL Custom]**, then **[!UICONTROL Moving Range]**. Use the fields and dropdowns at the top of the menu to set the range.
   * Click **[!UICONTROL Apply]** to save the interval and range settings.
   * Duplicate the `Items sold last 28 days` metric and open the new metric's `Time Options`. Set the options to the following:

      * `Time Interval`: leave this as `None`.
      * `Time Range`: change this to the date range that aligns with the promotion you are interested in by clicking **[!UICONTROL Specific Date Range]** and then entering the appropriate dates.
      * Rename the metric `Items sold during last promotion` or something similar.
      * Add your `Units on hand` metric.
      * Next, we need to add the calculations that show us the weeks on hand, considering sales trends, for the time periods (`last 7 days`, `last 28 days`, and `last promo` period) we are including in the report. You need to do this once for each time period.

To create the formulas, click **[!UICONTROL Add Formula]**. Enter the formulae below and click **[!UICONTROL Apply Changes]** when finished. Repeat this for each of the three time periods:

* For the `last 7 days time period`, enter `D / A` in the `Formula` field.
* For the `last 28 days time period`, enter `D / (B/4)` in the `Formula` field.

    >[!NOTE]
    >
    >It is important to normalize your selected time ranges here. Twenty-eight days should be broken into four weeks in this example. You may need to apply different logic to the formula.

* For the `last promo period`, enter `D / C` in the `Formula` field.

   ![](../assets/Different_Time_Ranges_2.png)

* Lastly, customize the report by hiding the metrics and adding a `SKU` or a similar dimension to the report as a `Group By`.

This example demonstrates that current inventory levels were well-situated for a product-wide 14-day sale. However, adding a comparable promotional period suggests that the company needs to make some changes – either by ordering more inventory and only promoting the items with enough units in stock.

Because your customers behave differently over time, you can expect to see variances in data when performing analyses. Setting custom Time Options enables you to quickly create complex analyses, enabling data-driven decisions that factor in historical trends.

See our [training video](https://support.magento.com/hc/en-us/articles/360016730071-Training-Video-Time-Options-in-the-Visual-Report-Builder) to learn more.
