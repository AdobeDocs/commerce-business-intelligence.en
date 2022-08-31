---
title: Understanding Results Between Database and SQL Editor
zendesk_id: 360016729891
---

You may be curious what the "Last successful update began" field is inside your Integrations page:

![Last_successful_update.png]({% link images/Last_successful_update.png %})

## Understand the timestamp field

It shows the start timestamp (in the timezone set on your account) of the _last successful update cycle_ on your account. Note that:

-  If any of the synced tables encountered an issue during the last update cycle, this timestamp is **not updated**.
-  Hence, there may be cases when reports have been updated with fresh data, but the "Last successful update began" is still lagging.

## Identify the "real" last data point

The latest data point for a particular integration is determined by the _Last Data Point Received_ timestamp located on the right of each integration. That timestamp refers to the last point at which your data warehouse successfully received data points from that source, whether it be a database, API, or third-party integration.

To check for freshness of data from **specific tables**, we recommend creating a quick [SQL report]({% link data-analyst/dev-reports/sql-rpt-bldr.md %}) that performs a **MAX(timestamp)** on the most important table on your account. Comparing this timestamp to the "Last Data Point" will indicate whether the issue affected the entire account or a subset of the tables. We recommend doing this for three to four important, commonly used tables.

-  If the MAX(timestamp) values are more recent than _Last Data Point Received_, it means that a subset of the tables were affected, but the overall account's update cycle is stable.
-  If the MAX(timestamp) values are equal to or before _Last Data Point Received_, it means that the account's update cycle was affected. In this situation, [submit a support ticket](https://support.magento.com/hc/en-us/articles/360019088251).
