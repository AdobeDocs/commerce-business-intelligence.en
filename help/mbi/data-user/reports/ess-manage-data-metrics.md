---
title: Create metrics
description: Learn how to use metrics to create charts.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
---
# Create metrics

>[!NOTE]
>
>Requires [Admin permissions](../../administrator/user-management/user-management.md).

A metric is a measurement. In SQL and database structures, a metric is like a stored query over a variable period.

In [!DNL Commerce Intelligence], you can use metrics to [create charts](../../data-user/reports/ess-rpt-build-visual.md). For example, the metric `revenue` is the total number of orders. The metric `average customer revenue per order` is what the average customer spends per order.

When used in reports, metrics can be analyzed over a specified time period and [filtered or segmented](../../best-practices/segment-filter.md) by different categories. Consider analyzing average customer revenue grouped by gender - in this case, `average customer revenue per order` is the metric and gender is the grouping.

## Defining the Metric {#define}

1. To create a metric, click **[!UICONTROL Data** > **Metrics]**.

1. Click **[!UICONTROL Create New Metric]**.

1. From the dropdown, click the table that includes the native or calculated column you want to use for your metric.

1. Name your metric.

    Adobe recommends a name that, at a glance, tells you what the metric is. For example: `Average Order Revenue`.

1. The next step is to define what your metric does. Using the dropdown menus, define the metric's operation, the `operation` column, and a `date` dimension:

    * Choose an operation:
       * `Count` - This operation counts the number of rows in a data table
       * `Max` - Max returns the maximum value of a specific data column
       * `Min` - Min returns the minimum value of a specific data column
       * `Sum` - This operation sums the values of a specific data column
       * `Average` - This operation calculates the average of the data column values
       * `Count Distinct Value` - This counts the unique number of values in a specific data column
       * `Median` - This operation calculates the median of the data column values
       * `First and Third Quartiles` - These operations calculate the 25th and 75th percentiles of the data column values, respectively
       * `Tenth and Ninetieth Percentiles` - These operations calculate the 10th and 90th percentiles of the data column values, respectively

    * Choose a column to perform the operation on. For example, if you wanted to find your total revenue, you would perform a sum operation on the `order total` column.

      If you are editing an existing metric, you can also [change the metric's operational table](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) in this section.

    * Choose a date dimension that can be used to trend the metric. For example, `order date`.

## Adding Filters {#filters}

The `Filter` section allows you to create a filter or apply a [saved filter set](../../data-user/reports/ess-manage-data-filters.md) to your metric.

For the `average order revenue` metric, you would not want to include any test orders that might have been done while setting up your store - this would give us an inaccurate result. Can apply a filter set to remove those orders from the data set. After the filter is created, it will apply to all charts built using this metric.

The `Filter Logic` section is where you can further define how a metric should behave.

* "\[`A`\] or \[`B`\]" allows any data that satisfy the filters \[`A`\] OR \[`B`\]
* "\[`A`\] and \[`B`\]" only allows data that satisfies both filters \[`A`\] and \[`B`\]
* "(\[`A`\] and \[`B`\]) OR \[`C`\]" only allows data that either satisfy both filters \[`A`\] and \[`B`\], or satisfies filter \[`C`\] alone

## Adding Dimensions {#dimensions}

The [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) section shows all available data dimensions for filtering or grouping; by default, all available data columns are listed as dimensions. Continuing the example, if you wanted to segment your revenue by referral source, you can do that here.

In addition to listing all available data columns as dimensions, [!DNL Commerce Intelligence] guesses at which columns are groupable. *To segment or group data on reports*, columns must be marked as groupable.

## Finishing Up {#finish}

In addition to defining how your metric behaves, you can also set permission levels in the `User Rights` section. While `Admin` users have access to all metrics, you have to indicate the users who can use this metric by checking the box next to the appropriate group.

If you are editing an existing metric, you can view a list of charts (and who owns them) that use this metric in the `Dependent Charts` section.

Changes are saved automatically and your metric is now good to go.
