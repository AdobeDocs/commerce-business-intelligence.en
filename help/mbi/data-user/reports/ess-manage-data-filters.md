---
title: Create filter sets for metrics
description: Learn how to create saved Filter Sets and apply them to the metrics.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
---
# Create filter sets

If you have multiple metrics in [!DNL Commerce Intelligence] that need to be filtered in a similar way (for example, filter out test orders), you can create saved Filter Sets and apply them to the metrics. This saves you time as you do not have to add individual filters when creating or editing a metric.

See the [training video](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) for more information.

>[!NOTE]
>
>Requires [Admin permissions](../../administrator/user-management/user-management.md).

1. Click **[!DNL Manage Data** > **Filter Sets]** in the sidebar.

    ![](../../assets/create-filter-sets.png)

1. Click **[!UICONTROL Add Filter Set]** at the top of the page.

1. Select the table that contains the metrics you want to filter.

   For example, if you want to filter your `Total number of orders` metric and it is built on the `orders` table, select that table.

1. Name the `Filter Set`.

1. Add all relevant filters.

    For example, if you only wanted to include orders with a status of complete in your `Total number of orders` metric, you would apply a filter that excludes all orders that do not have status = `complete`.

1. Verify your filter logic and that parentheses and operators are placed correctly: for example, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   An incorrect filter is often the cause of data discrepancies between [!DNL Commerce Intelligence] reports and your expected results.

1. Save the `Filter Set`.

After a filter set is saved, you can apply it to any metric that is using the same table. For example, if you created a `Filter Set` on the `orders` table, you can apply it to *any metrics* built on this table, such as `Revenue`.

>[!NOTE]
>
>`Filter Sets` can also be applied to calculated columns in [!DNL Commerce Intelligence]. You may request to apply a filter set to a data dimension created in [!DNL Commerce Intelligence] via by contacting support.

## Related

* [Best Practices for Segmentation and Filtering](../../best-practices/segment-filter.md)
