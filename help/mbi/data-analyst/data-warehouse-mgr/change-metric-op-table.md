---
title: Change a metric's operational table
description: Learn how to change the data table that a metric uses to perform its operation.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Change a metric's operational table

In certain cases, you may decide to change the data table that a metric uses to perform its operation. For example, if you have a new users table, you want to migrate your user-related metrics from the  `Users\_Old` table to use the `Users\_New` table instead.

1. Go to **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Click **[!UICONTROL Edit]** beside the metric for which you would like to switch the `operational` table.
1. In the editor, click **[!UICONTROL Change]**.

    ![Metric definition page showing operational table setting](../../assets/change-metrics-1.png)
1. Select the new table that you would like to base this metric on.
1. Match existing data dimensions to corresponding ones in the new table. For example, if you had a column called `User's registration date`, simply select which column in the new table records the same date data. (See next step if you do not have matching columns in the new table)

    ![Table selection dropdown showing available tables](../../assets/change-metrics-2.png)

1. If you do not have a matching column in the new table, you can either **create it in your data table** or [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) if it is a calculation column or dimension made by [!DNL Commerce Intelligence]. You can also **delete the dimension from the metric**. To delete a dimension that you no longer need, simply go back to the metric's editor and select which dimensions to delete under `Dimensions`.

    ![Operational column selection dropdown menu](../../assets/change-metrics-3.png)
