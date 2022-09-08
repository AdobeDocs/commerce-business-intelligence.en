---
title: Expected Mixpanel data
zendesk_id: 360016504312
---

After [you’ve connected your Mixpanel account](../data-analyst/importing-data/integrations/mixpanel.md), you can use the [Data Warehouse Manager](../data-analyst/data-warehouse-mgr/tour-dwm.md %}#syncing) to easily track relevant data fields for analysis.

In this article, we’ll explore the main data tables that you can import from Mixpanel into your Magento BI account. The following tables will be created in your data warehouse after connecting Mixpanel. To view all the fields available for tracking, click the links in the table name column.

Note that due to the limitations of Mixpanel\'s API, historical data - data older than seven (7) days from the date of connection to Magento BI - will not be replicated.

| **Table Name** | **Description** |
| [mixpanel\_export](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | This table contains raw event data, including the event, event dates, and platform bucket. |
| [mixpanel\_funnels](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | This table contains data about your funnels, including the funnel ID, the funnel length (# of days the user has to complete the funnel), and the starting and ending dates of the funnel. |
| [mixpanel\_engage](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | This contains data from People Analytics, including session IDs, page and user information, and the date/time the user was last seen.  |

## Related documentation

* [Connecting Mixpanel](../data-analyst/importing-data/integrations/mixpanel.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
