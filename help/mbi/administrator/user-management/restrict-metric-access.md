---
title: Restrict metrics access
description: Learn how to work with metrics access and restrictions. 
---
# Manage metrics users

In addition to setting user permission levels, you can also restrict access to metrics on a user-by-user basis. For example, if you want your accounting department to have access to revenue-related metrics but not user-acquisition metrics, you can restrict access to those metrics.

In cases like these, we recommend setting that user's account to [Standard](../../administrator/user-management/user-management.md). Standard permissions should be given to users who do not need to create or alter metrics, calculated columns, integrations, or users, but they do need access to data in the Data Warehouse. If you want to fully restrict access to data, use the **Read Only** permissions instead.

After setting the permission level, you can select the metrics a Standard user can access by doing the following:

1. Go to **Account Settings > Manage Users.**
1. Select the desired user account.
1. The **Metrics** tab will display a list of available metrics. Check the metrics that you want the user to have access to; deselect those the user should not have access to.
1. [!DNL MBI] saves the changes automatically. If the change is successful, [!DNL MBI] displays **Saved!** at the top of the page.

>[!NOTE]
>
>All users with Standard permissions can access all data in the data warehouse via Data Export in addition to all metrics from Google Analytics.

You can also restrict access to a metric by editing the metric and [selecting users in the User Rights section](../../data-user/reports/ess-manage-data-metrics.md).

>[!NOTE]
>
>If you duplicate a metric, [!DNL MBI] copies the user permissions set in the original metric.
