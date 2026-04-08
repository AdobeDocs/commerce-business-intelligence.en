---
title: Working with SQL Report Builder
description: Learn how to audit data and metrics using the SQL Report Builder so that you can compare the results with the data from your local database.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Developer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
TQID: https://experienceleague.adobe.com/7Yx7Kpir-xjz5TPuajN7CFsLjWAbY0AT3bKtBabA5Wk
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
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
---
# [!DNL SQL Report Builder]

The [!DNL SQL Report Builder] is primarily used to build new reports and iterate on analyses, but it can also be used to effectively audit data and metrics. The following information explains how to audit data and metrics using the [!DNL SQL Report Builder] so that you can compare the results with the data from your local database.

## Querying a metric

To get started, open the [!DNL SQL Report Builder] by navigating to **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. You can use the sidebar in the [!DNL SQL] editor to insert a metric directly into your query by hovering over the metric and clicking **[!UICONTROL Insert]**. This adds the query definition of that metric to the editor. The definition includes the following components:

- The **metric operation** being performed, indicated by `SUM()` in the example below.
- The **table on** which the metric is built, indicated by the `FROM` clause.
- Any **filters (and filter sets)** that have been added to the metric, indicated by the `WHERE` clause in the example below.
- The component of the **timestamp** (year, month) on which the data is to be ordered, indicated by the `ORDER BY` clause in the example below.

To have a clearer view of the query, you can reformat how it is displayed in the query field. When ready, select `Run Query`. The results populate as a table in the report panel below the query.

![Animated demonstration of running SQL query and viewing results](../../assets/run-query-results.gif)

## Restricting the query

If you are trying to pinpoint a specific discrepancy or set of data, you should restrict the query to a specific sample to check against your local database. You can do this by editing the query to match your desired restrictions. In the following example, you are restricting the query to include only revenue from January 1, 2013 or later. After you update the query, select **[!UICONTROL Run Query]** again to update the results.

![Animated demonstration of restricting query with filters](../../assets/restricting-query.gif)

## Saving and exporting

When the report meets your needs, give the report a distinct name, click **[!UICONTROL Save]**, and select the type of report you would like to save and the dashboard. When auditing metrics, Adobe recommends saving the report as a `Table` and saving it to a test dashboard.

After the report is saved, navigate to that dashboard by selecting `Go to Dashboard`. From there, you can export the data by finding the report and selecting **[!UICONTROL Options gear > Full `.csv` Export]** or **[!UICONTROL Full Excel Export]**.

![Animated demonstration of exporting dashboard data](../../assets/export-dboard-data.gif)

## Custom queries

You can also write custom queries and export the results to compare against your local database. Following the [guidelines for query optimization](../../best-practices/optimizing-your-sql-queries.md), write a query in the SQL editor. You can use the buttons at the top of the sidebar to toggle between lists of tables and metrics available for use in the [!DNL SQL Report Builder] and add them to your query. When your custom query fits your needs, you can save the report and export that data from the dashboard.

>[!NOTE]
>
>If you find a discrepancy after auditing your data, look at the [Contacting Support: Data Discrepancies](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) support topic for more information on what to do next.
