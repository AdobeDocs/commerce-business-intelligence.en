---
title: Managing data dimensions
description: Learn how data is generated, what exactly causes a new row to be inserted into one of the Core Magento Tables, and how are actions such as making a purchase or creating an account recorded into the Magento database.
---
# Managing data dimensions

>[!NOTE]
>
>[Requires Admin permissions](../../administrator/user-management/user-management.md)

A dimension is a field in the same table as a metric that can be used to filter or segment charts based on that metric. For example, a revenue metric may contain city, state, country, order status, coupon code and other types of dimensions.

## Add dimensions to multiple metrics

To add one or more dimensions to multiple Metrics at once:

1. On the main navigation bar, go to **Manage Data > Metrics**.

1. At the top of the page, click **Add Dimensions To Metric(s)**.

1. Choose the table that contains the dimensions.

1. In the _Choose Metric(s) to Add Dimensions_ column, select the metrics you want to add dimensions to. Once selected, the _Choose Dimensions to Add_ column will appear on the right. Check the dimensions you want to add to the selected metric.

   ![](../../assets/Add_Dimensions.png)

1. If you would like to segment or group by any of the data dimensions on reports, make sure to indicate they are _Groupable_.

1. Click **Add**.

## Delete dimensions from multiple metrics

To delete one or more dimensions from multiple metrics:

1. On the main navigation bar, go to **Data > Metrics**.

1. At the top of the page, click **Remove Dimensions From Metric(s)**.

1. Choose the table that contains the dimensions.

1. Select the metrics you would like to remove the dimensions from on the left, and the dimensions you wish to remove on the right.

1. Click **Remove**.

1. If the dimensions are in use on reports, you will be shown a warning and a list of charts that are using the dimensions. Click **Delete** to delete the checked dimensions and all of their dependents, including reports.

## Manage dimensions in metrics

**To add dimension(s) in a metric:**

1. On the main navigation bar, go to **Data > Metrics**.

1. Click **Edit** on the metric you want a new dimension.

1. Under the _Dimensions_ section, use the _Add a dimension_ dropdown to select a dimension to add.

>[!NOTE]
>
>Any dimension that you want to filter or group by must already be tracked in MBI. If you do not find the desired dimension, we may need to start tracking a new data column in your database via the [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) page.


**To delete dimension(s) from a metric:**

1. On the main navigation bar, go to **Manage Data > Metrics**.

1. Click **Edit** on the metric you want a new dimension.

1. Under the _Dimensions_ section, select the checkbox in the delete column next to the dimension(s) you wish to remove.

>[!NOTE]
>
>Even after deleting a dimension, it still exists as a column on your table in our data warehouse. You can add it back to any metric, and build new metrics using these dimensions. To remove the data column a dimension corresponds to from MBI, simply untrack the data column via the [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) page.

## Related documentation

* [Best Practices for Segmentation and Filtering](../../best-practices/segment-filter.md)
