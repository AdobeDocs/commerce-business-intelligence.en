---
title: Managing data dimensions
description: Learn what a dimension is and it can be used to filter or segment charts based on a metric.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/0q2fVRWwNd21eyyO7WyYKlENLArkw325oq4YLNIRfLg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Managing data dimensions

>[!NOTE]
>
>Requires [Admin permissions](../../administrator/user-management/user-management.md).

A dimension is a field in the same table as a metric that can be used to filter or segment charts based on that metric. For example, a revenue metric may contain city, state, country, order status, coupon code, and other types of dimensions.

## Add dimensions to multiple metrics

To add one or more dimensions to multiple Metrics at once:

1. Go to **[!UICONTROL Manage Data > Metrics]**.

1. Click **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Choose the table that contains the dimensions.

1. In the `Choose Metric(s) to Add Dimensions` column, select the metrics you want to add dimensions to. Once selected, the `Choose Dimensions to Add` column appears on the right. Check the dimensions that you want to add to the selected metric.

   ![Add Dimensions dialog showing available dimension options](../../assets/Add_Dimensions.png)

1. If you would like to segment or group by any of the data dimensions on reports, make sure to indicate they are _Groupable_.

1. Click **[!UICONTROL Add]**.

## Delete dimensions from multiple metrics

To delete one or more dimensions from multiple metrics:

1. Go to **[!UICONTROL Data > Metrics]**.

1. Click **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Choose the table that contains the dimensions.

1. Select the metrics that you would like to remove the dimensions from on the left, and the dimensions you wish to remove on the right.

1. Click **[!UICONTROL Remove]**.

1. If the dimensions are in use on reports, a warning displays with the list of charts that are using the dimensions. Click **[!UICONTROL Delete]** to delete the checked dimensions and all of their dependents, including reports.

## Manage dimensions in metrics

**To add dimension(s) in a metric:**

1. Go to **[!UICONTROL Data > Metrics]**.

1. Click **[!UICONTROL Edit]** on the metric you want a new dimension.

1. In the `Dimensions` section, use the `Add a dimension` dropdown to select a dimension to add.

>[!NOTE]
>
>Any dimension that you want to filter or group by must already be tracked in [!DNL Commerce Intelligence]. If you do not find the desired dimension, you may need to start tracking a new data column in your database via the [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) page.


**To delete dimension(s) from a metric:**

1. Go to **[!UICONTROL Manage Data > Metrics]**.

1. Click **[!UICONTROL Edit]** on the metric you want a new dimension.

1. Under the `Dimensions` section, select the checkbox in the delete column next to the dimension(s) you wish to remove.

>[!NOTE]
>
>Even after deleting a dimension, it still exists as a column on your table in your Data Warehouse. You can add it back to any metric, and build new metrics using these dimensions. To remove the data column that a dimension corresponds to from [!DNL Commerce Intelligence], simply untrack the data column via the [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) page.

## Related documentation

* [Best Practices for Segmentation and Filtering](../../best-practices/segment-filter.md)
