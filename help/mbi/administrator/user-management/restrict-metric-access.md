---
title: Restrict metrics access
description: Learn how to work with metrics access and restrictions.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
TQID: https://experienceleague.adobe.com/e87ix3NAqY6xZQbNbQkXuCnvvH2B-8H3APYpKtshs9w
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: 'Admin tools and workspace '
subfeature_v2:
  - id: a5fafba0-d4b6-446a-93b4-ff47bde7657e
    internal-label: 'Admin dashboard '
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
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
