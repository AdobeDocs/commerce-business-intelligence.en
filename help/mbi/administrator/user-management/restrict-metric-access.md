---
title: Restrict metrics access
description: Learn how to work with metrics access and restrictions.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
---
# Manage metrics users

In addition to setting user permission levels, you can also restrict access to metrics on a user-by-user basis. For example, if you want your accounting department to have access to revenue-related metrics but not user-acquisition metrics, you can restrict access to those metrics.

In cases like these, Adobe recommends setting that user's account to **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** permissions should be given to users who do not need to create or alter metrics, calculated columns, integrations, or users, but they do need access to data in the Data Warehouse. If you want to fully restrict access to data, use the **[!UICONTROL Read Only]** permissions instead.

After setting the permission level, you can select the metrics a **[!UICONTROL Standard]** user can access by doing the following:

1. Go to **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Select the desired user account.
1. The **[!UICONTROL Metrics]** tab displays a list of available metrics. Check the metrics that you want the user to have access to and deselect those that the user should not have access to.
1. [!DNL Adobe Commerce Intelligence] saves the changes automatically. If the change is successful, [!DNL Commerce Intelligence] displays **[!UICONTROL Saved!]** at the top of the page.

>[!NOTE]
>
>All users with **[!UICONTROL Standard]** permissions can access all data in the Data Warehouse via Data Export in addition to all metrics from [!DNL Google Analytics].

You can also restrict access to a metric by editing the metric and **[!UICONTROL Standard]** selecting users in the **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** section.

>[!NOTE]
>
>If you duplicate a metric, [!DNL Commerce Intelligence] copies the user permissions set in the original metric.
