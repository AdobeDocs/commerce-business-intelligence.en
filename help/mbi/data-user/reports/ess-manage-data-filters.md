---
title: Creating filter sets for metrics
zendesk_id: 360016505492
---

If you have multiple metrics in MBI that need to be filtered in a similar way (e.g., filter out test orders), you can create saved Filter Sets and apply them to the metrics. This saves you time as you do not have to add individual filters when creating or editing a metric.

See our [training video](https://support.magento.com/hc/en-us/articles/360016730151) to learn more.

{:.bs-callout-info}
[Requires Admin permissions](../../administrator/user-management/user-management.md)

1. Click **Manage Data** > **Filter Sets** in the sidebar.

    ![](../../assets/create-filter-sets.png)

1. Click **Add Filter Set** at the top of the page.

1. Select the table that contains the metrics you want to filter.

   For example, if you want to filter your **Total number of orders** metric and it is built on the **orders** table, select that table.

1. Name the Filter Set.

1. Add all relevant filters.

    For example, if we only wanted to include orders with a status of complete in our **Total number of orders** metric, we would apply a filter that excludes all orders that do not have status = complete.

1. Verify your filter logic and that parentheses and operators are placed correctly: e.g., `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   An incorrect filter is often the cause of data discrepancies between MBI reports and your expected results.

1. Save the Filter Set.

After a filter set is saved, you can apply it to any metric that is using the same table. For example, if you created a Filter Set on the _orders_ table, you can apply it to **any metrics** built on this table, such as **Revenue.**

Note that Filter Sets can also be applied to calculated columns in MBI. You may request to apply a filter set to a data dimension created in MBI via by contacting support.

## Related

* [Best Practices for Segmentation and Filtering](../../best-practices/segment-filter.md)
