---
title: Use the Visual Report Builder
description: Learn to analyze the data in your report for a specific time period.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
---
# Use the [!DNL Visual Report Builder]

The [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) allows you to visually explore your data to draw insights and help drive business decisions. This tutorial walks you through the process of creating a basic report.

>[!NOTE]
>
>To add a report to a dashboard, you need `Standard` [user permissions](../administrator/user-management/user-management.md) and `Edit` access to the dashboard.

## Step 1: Creating a Report

To get started creating a report, click **[!UICONTROL Report Builder]** on the sidebar or **[!UICONTROL Add Report]** at the top of any dashboard. When the `Report Builder` page displays, click the **[!UICONTROL Visual Report Builder]** option.

To edit a report created in the [!DNL Visual Report Builder], click the gear (Options) icon in the upper-right corner of any chart, then click **[!UICONTROL Edit]**.

## Step 2: Adding Metrics

The first step in creating an analysis is selecting [the metric](../data-user/reports/ess-manage-data-metrics.md) to analyze. While the metrics are listed alphabetically by default, you can also group them by the table that powers the metric.

You can add additional metrics after the initial metric is selected and overlay all the metrics on a single report or perform multi-metric calculations by adding formulas.

## Step 3: Adding `Formulas`

`Formulas` are added to reports by clicking **[!UICONTROL Add Formula]**, located just above the list of metrics in the report. In the [formula editor](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), any of the metrics included in the report can be used as inputs. Basic mathematical operators are used to manipulate the different metrics.

Say you wanted to create a report that shows us the average revenue per order. In this case, you would divide the `Revenue` metric by the `Number of orders` metric.

![Use the Visual Report Builder](../assets/ave-rev-per-order.png)

## Step 4: Setting the `Time Period` and `Interval of Analysis` {#time}

To zero in on a particular stretch of time, you can set the time period for the analysis. You can also choose time intervals to segment the data (for example, by year, by quarter, or by month). Use the menus in the top-right corner of the chart to set the time period and interval.

![Use the Visual Report Builder](../assets/Time_Options_Report_Builder.png)

When setting a specific date range for the time period, make sure that the start date is at the beginning of the interval and the end date is at the end of your interval.

For example, setting a time period from `January 1st` to `March 1st` and choosing a `monthly` interval shows `March` as a datapoint, but ignore every day in `March` except `March 1`. In that case, you should make your `Time Period` from `January 1 to March 31`.

## Step 5: `Group by` / `Segmenting the Analysis` {#groupby}

[To segment your metrics by a data dimension](../best-practices/segment-filter.md), click the **[!UICONTROL Group by]** menu at the top left of the chart. This reveals a dropdown including all available dimensions of the first metric included in the list.

You can choose `None` to prevent a metric from being segmented. For example, you might want a metric that returns total revenue without being segmented, while having another revenue metric segmented by region.

Go back to your average revenue per order example and set the Group by to promo code. This shows you the average revenue per order for orders both with and without a promo code.

![Use the Visual Report Builder](../assets/Group_By_Report_Builder.png)

If the metrics included in the analysis are built on different data tables, a pop-up allows you to select the matching data dimension in each table. The goal here is to find dimensions that share type of values for segmentation:

![Use the Visual Report Builder](../assets/Dimension_Editor.png)

## Step 6: Setting `Metric Filters`, `Perspective`, and `Time Interval` {#metric-specific}

For each metric added to the analysis, you can add filters, select the relevant data perspective, and set `time interval` options. To access these features, click the funnel (`Filter`), eye (`Perspective`), and clock (`Time`) icons located next to the metrics included in the report.

![Use the Visual Report Builder](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` limit the dataset included in the analysis. Filters are useful, for example, when evaluating individual acquisition channels and removing outliers.

In addition to the dropdown menus and text box, you can also use special filter operators such as `LIKE` or `IN` to create filters.

The use of wildcards (`%` or `_`) with `LIKE` statements is supported. The `%` wildcard matches multiple characters, while `_` only matches any single character. For example:

- `affiliate's name Like B%` only allows data from customers whose name starts with `B`.

- `affiliate's name Like _ake` only allows data from customers whose names are something like `Jake`, `Rake`, or `Bake` but not `Drake` or `Blake`.

Adding multiple filters allows tight control of the chart's data. By default, all filter conditions must be true for a piece of data to be included, but you can create OR relationships by editing the Filter Rules text box.

![Use the Visual Report Builder](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` Allow you to easily toggle between different views of your data. Look at what is available:

- `Standard perspective`: The standard perspective shows you the result for the matching date on the x-axis (for example revenue in January). This is the perspective that you use in your Average revenue per orders example.

![Use the Visual Report Builder](../assets/Standard.png)

- `Amount` OR `Percent Change` versus `Previous Period` perspective: This perspective shows the amount or percent change from one interval to the next and is useful for measuring the rate of change in fast-changing metrics. There is also a perspective to compare the interval to the same time period last year to show year over year growth.

![Use the Visual Report Builder](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: The `cumulative perspective` shows the ongoing or cumulative sum amount of the metric over the time period. This is often used to analyze total customers and plan for future capacity.

![Use the Visual Report Builder](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: This perspective shows the data as a percentage of the first-time interval included in the analysis. This is helpful in measuring the effectiveness of specific actions relative to the first period performance.

![Use the Visual Report Builder](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: The rolling averages window perspective shows the rolling average value of a metric over the specified time range. The interval must be the same as the interval set on the report level. For example, if the report is showing the last full quarter of Revenue by week, you can set the rolling average window time range to four weeks. This makes the first three values are null and the fourth value represents the average of the first four weeks of Revenue. For clarity, make sure to turn off the `Multiple Y-Axes` checkbox if you are viewing the same metric with a rolling average, like in the example below.

![Use the Visual Report Builder](../assets/rolling_avg_window.png)

### Metric-specific Time Options

Two options exist for metrics used in reports: they can trend over time according to the global time options, or not, which will display them as a scalar number.

Changing a metric time interval to `None` returns a `scalar` number, which is useful when creating formulas that involve dividing a time-trending metric by a `scalar` number. Also, you can also change the time range of the `scalar` metric to a time range independent of that for the report.

Say, for example, you wanted to see 2019 monthly revenue expressed as a percentage of overall 2019 revenue. You can add two `Revenue` metrics to a report with a global time range of January 1, 2019, to December 31 2019, segmented by monthly interval.

>[!NOTE]
>
>If you add `group by` dimensions, choose a new visualization, or adjust the time interval and then save just the Number (`scalar`). Those adjustments are not kept the next time you open that report from a dashboard - only the time range will be kept.

To learn more about using time options in your reports, see this [tutorial](../tutorials/time-options-visual-rpt-bldr.md).

## Step 7: Saving the Report

When you create a chart, you can save it by clicking **[!UICONTROL Save]** at the top-right corner of the `Visual Report Builder`.

You can choose to save a chart, table, or number (`scalar`) using the `Type` dropdown and the dashboard to which the report should be saved using the `Location` dropdown.

You can then save the report by clicking **[!UICONTROL Save to Dashboard]**.

![Use the Visual Report Builder](../assets/save-to-dashboard.png)

## Report Outputs

To help you decide which report output to choose, see the following:

### Chart

![Use the Visual Report Builder](../assets/RB_Chart.png)

### Table

![Use the Visual Report Builder](../assets/RB_Table.png)

### Number (`scalar`)

![Use the Visual Report Builder](../assets/RB_Scalar.png)

Congratulations! You are finished.
