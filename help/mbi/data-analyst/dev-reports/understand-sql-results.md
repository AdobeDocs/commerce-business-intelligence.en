---
title: Understanding Results Between Database and SQL Editor
zendesk_id: 360016733051
---

The majority of the time, differences in results can be attributed to update cycles. If MBI is in the process of replicating data from your database to your Data Warehouse, you might see different results even when using the same query.

Connection issues can also result in discrepancies. Navigate to the Connections page (**Manage Data > Connections**) to check it out - is there an error for the database integration in question? If so, you may need to [reauthenticate the integration](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations) to get things running again.

If all your integrations are connected successfully and you are not in the middle of an update cycle, something else may be amiss. Try using the [data discrepancy troubleshooting guides](https://support.magento.com/hc/en-us/sections/360003074492) on our Support site to pinpoint the problem.
