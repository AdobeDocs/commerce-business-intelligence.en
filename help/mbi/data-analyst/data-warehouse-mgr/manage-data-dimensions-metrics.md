---
title: Managing data dimensions in metrics
zendesk_id: 360016505892
---

A dimension is a field in the same table as a metric that can be used to filter or segment charts based on that metric. For example, a revenue metric may contain city, state, country, order status, coupon code and other types of dimensions.
{: dir="ltr"}

Note: To manage dimensions, you must have administrative access.
{: dir="ltr"}

## Add dimensions to multiple metrics
{: dir="ltr"}

To add one or more dimensions to multiple Metrics at once:

1. {: dir="ltr"} On the main navigation bar, go to **Manage Data &gt; Metrics. **
    {: dir="ltr"}

1. {: dir="ltr"} At the top of the page, click "Add Dimensions To Metric(s)".
    {: dir="ltr"}

1. {: dir="ltr"} Choose the table that contains the dimensions.
    {: dir="ltr"}

1. {: dir="ltr"} In the **Choose Metric(s) to Add Dimensions** column, select the metrics you want to add dimensions to. Once selected, the **Choose Dimensions to Add** column will appear on the right. Check the dimensions you want to add to the selected metric.![](../../assets/Add_Dimensions.png)
1. {: dir="ltr"} If you would like to segment or group by any of the data dimensions on reports, make sure to indicate they are Groupable.
    {: dir="ltr"}

1. {: dir="ltr"} Click "Add".

## Delete dimensions from multiple metrics
{: dir="ltr"}

To delete one or more dimensions from multiple metrics:

1. {: dir="ltr"} On the main navigation bar, go to Data&gt;Metrics.
    {: dir="ltr"}

1. {: dir="ltr"} At the top of the page, click "Remove Dimensions From Metric(s)".
    {: dir="ltr"}

1. {: dir="ltr"} Choose the table that contains the dimensions.
    {: dir="ltr"}

1. {: dir="ltr"} Select the metrics you would like to remove the dimensions from on the left, and the dimensions you wish to remove on the right.
    {: dir="ltr"}

1. {: dir="ltr"} Click "Remove".
    {: dir="ltr"}

1. If the dimensions are in use on reports, you will be shown a warning and a list of charts that are using the dimensions. Use the "Delete" button to delete the checked dimensions and all of their dependents, including reports.

## Manage dimensions in metrics
{: dir="ltr"}

**To add dimension(s) in a metric:**

1. {: dir="ltr"} On the main navigation bar, go to Data&gt;Metrics.
    {: dir="ltr"}

1. {: dir="ltr"} Click "Edit" on the metric you want a new dimension.
    {: dir="ltr"}

1. {: dir="ltr"} Under the "Dimensions" section, use the "Add a dimension" dropdown menu to select a dimension to add.
    {: dir="ltr"}

Note that any dimension that you want to filter or group by must already be tracked in MBI. If you do not find the desired dimension, we may need to start tracking a new data column in your database via the [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) page.
{: style="padding-left: 30px;"}

**To delete dimension(s) from a metric:**
{: dir="ltr"}

1. {: dir="ltr"} On the main navigation bar, go to **Manage Data &gt; Metrics. **
    {: dir="ltr"}

1. {: dir="ltr"} Click "Edit" on the metric you want a new dimension.
    {: dir="ltr"}

1. {: dir="ltr"} Under the "Dimensions" section, select the checkbox in the delete column next to the dimension(s) you wish to remove.
    {: dir="ltr"}

Note that even after deleting a dimension, it still exists as a column on your table in our data warehouse. You can add it back to any metric, and build new metrics using these dimensions. To remove the data column a dimension corresponds to from MBI, simply untrack the data column via the [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) page.

## Related documentation

* [Best Practices for Segmentation and Filtering](../../best-practices/segment-filter.md)
