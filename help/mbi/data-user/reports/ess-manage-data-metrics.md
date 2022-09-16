---
title: Creating metrics
zendesk_id: 360016504592
---

{:.bs-callout-info}
[Requires Admin permissions](../../administrator/user-management/user-management.md)

Simply put, a metric is a measurement. In SQL and database structures, a metric is like a stored query over a variable period of time.

In MBI, you can use metrics to [create charts](../../data-user/reports/ess-rpt-build-visual.md). For example, the metric **revenue** is the total amount of orders. The metric **average customer revenue per order** is what the average customer spends per order.

When used in reports, metrics can be analyzed over a specified time period and [filtered or segmented](../../best-practices/segment-filter.md) by different categories. Consider analyzing average customer revenue grouped by gender - in this case, **average customer revenue per order** is the metric and gender is the grouping.

## Defining the Metric {#define}

1. To create a new metric, click **Data > Metrics**.

1. Click **Create New Metric**.

1. From the dropdown, click the table that includes the native or calculated column you want to use for your metric.

1. Name your metric.

    We recommend a name that, at a glance, tells you what the metric is. For example: _Average Order Revenue_.

1. The next step is to define what your metric does. Using the drop-down menus, define the metric's operation, the operation column, and a date dimension:

    * Choose an operation:
       * **Count** - This operation counts the number of rows in a data table
       * **Max** - Max returns the maximum value of a specific data column
       * **Min** - Min returns the minimum value of a specific data column
       * **Sum** - This operation sums the values of a specific data column
       * **Average** - This operation calculates the average of the data column values
       * **Count Distinct Value** - This counts the unique number of values in a specific data column
       * **Median** - This operation calculates the median of the data column values
       * **First and Third Quartiles** - These operations calculate the 25th and 75th percentiles of the data column values, respectively
       * **Tenth and Ninetieth Percentiles** - These operations calculate the 10th and 90th percentiles of the data column values, respectively

    * Choose a column to perform the operation on. For example, if you wanted to find your total revenue, you would perform a sum operation on the **order total** column.

      If you're editing an existing metric, you can also [change the metric's operational table](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) in this section.

    * Choose a date dimension that can be used to trend the metric. For example, **order date**.

## Adding Filters {#filters}

The Filter section allows you to create a new filter or apply a [saved filter set](../../data-user/reports/ess-manage-data-filters.md) to your metric.

For our **average order revenue** metric, we would not want to include any test orders that might have been done while setting up our store - this would give us an inaccurate result. We can apply a filter set to remove those orders from the data set. After the filter is created, it will apply to all charts built using this metric.

The Filter Logic section is where you can further define how a metric should behave.

* "\[A\] or \[B\]" will allow any data that satisfy the filters \[A\] OR \[B\]
* "\[A\] and \[B\]" will only allow data that satisfies both filters \[A\] and \[B\]
* "(\[A\] and \[B\]) OR \[C\]" will only allow data that either satisfy both filters \[A\] and \[B\], or satisfies filter \[C\] alone

## Adding Dimensions {#dimensions}

The [Dimensions](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) section shows all available data dimensions for filtering or grouping; by default, all available data columns are listed as dimensions. Continuing our example, if we wanted to segment our revenue by referral source, we could do that here.

In addition to listing all available data columns as dimensions, MBI will also take a guess at which columns are groupable. **To segment or group data on reports**, columns must be marked as groupable.

## Finishing Up {#finish}

In addition to defining how your metric behaves, you can also set permission levels in the _User Rights_ section. While Admin users have access to all metrics, you have to indicate the users who can use this metric by checking the box next to the appropriate group.

If you're editing an existing metric, you can view a list of charts (and who owns them) that use this metric in the _Dependent Charts_ section.

Changes are saved automatically and your metric is now good to go.
