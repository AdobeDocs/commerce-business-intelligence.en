---
title: Using Dashboard Wide Filtering
zendesk_id: 360016503192
---

With dashboard wide filtering, you can make bulk edits of all the reports on a specific dashboard. You can quickly view the same analysis over different time periods or for different stores. You can easily compare the performance of a previous year, month, or week per store. Further, you can update an entire dashboard to accommodate a newly launched campaign.

## Date filters

To change the date range or interval of reports on a dashboard, click the calendar icon in the upper-right-hand corner (![calendar-button.png](../../assets/calendar-button.png)).

You can choose to view data using a **Fixed Date Range** or a variety of pre-calculated **Moving Date Ranges**:

![moving\_date\_ranges.png](../../assets/moving_date_ranges.png){: width="330" height="407"}

The `Last Full...` moving range options represent the most recently fully completed range, while `This...` will be the current, in-progress range. For example, if it is currently June, the `Last Full Month` is _May 1 - May 31_, while `This Month` is _June 1 - Now_.

Or create your own **Custom Moving Range**\:

![custom-moving-range.png](../../assets/custom-moving-range.png)

Choose to change the interval as well. Selecting the default button (![time_interval_default.png](../../assets/time_interval_default.png)) means only the date range will be changed:

![time_interval.png](../../assets/time_interval.png){: width="330" height="407"}

To restore all reports to their initial date range and interval, click <span class="btn">Restore Defaults</span>, or click <span class="btn">Cancel</span>.

When you specify a date filter for a dashboard, that filter is applied to that dashboard only. It is not applied when you navigate to other dashboards.

{:.bs-callout-info}
At this time, **Cohort Reports** and **SQL Reports** are not included when applying changes at a dashboard level.

## Store filters

To analyze how a specific store is performing, click the stores icon in the upper-right-hand corner (![Store Filter](../../assets/store-filter.png)). By default, **Store Filter** is set to `All Stores`, which displays the data from all [store views](https://docs.magento.com/user-guide/stores/stores-all-create-view.html) available in your Commerce site.

{:.bs-callout-info}
A store filter is enabled or disabled for an entire MBI account. If a dashboard contains reports that are not affected by the filter, such as reports that are not built on any Commerce data, those reports do not update when the store filter is applied. You can [contact support](../../getting-started/support.md) if you believe a report should update based on store selection or if you believe your account store filter is mistakenly disabled.

When you select a store from the **Store Filter**, the filter retains your selection when you navigate between dashboards. Retaining your selection allows you to see data for your selected store everywhere until you select `All Stores`.

## Filters for shared dashboards

For shared dashboards, if one user configures the date filter, other users with access to the dashboard will see that same filter applied. However, the store filter does not apply in this case. If the dashboard owner configures the store filter and shares the dashboard, the configured store filter will not persist to another user. A user must have [edit access](../../data-user/dashboards/share-dashboard-with-users.md) to a dashboard in order to adjust the dashboard filters.
