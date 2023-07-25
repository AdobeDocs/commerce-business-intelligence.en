---
title: Using the SQL Report Builder
description: Learn the ins and outs of using the SQL Report Builder.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
---
# Using [!DNL SQL Report Builder]

>[!NOTE]
>
>Requires [Admin permissions](../../administrator/user-management/user-management.md) to create and edit SQL charts. `Standard` users can rearrange these charts on dashboards, and `Read-only` users have the same experience they do with traditional charts. In addition, `Read-only` users do not have access to the text of the query.

See the [training video](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) to learn more.

[!DNL SQL], or Structured Query Language, is a programming language used to communicate with databases. In [!DNL Commerce Intelligence], [!DNL SQL] is used to query, or retrieve, data from your Data Warehouse. Look at the reports on your dashboard - behind the scenes, each one is powered by a [!DNL SQL] query.

You can use the [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) to directly query your Data Warehouse, view the results, and transform them into a chart. You can start creating a report with the [!DNL SQL Report Builder] by clicking **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

See the [training video](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) to learn more.

The [!DNL SQL Report Builder] allows you to directly query your Data Warehouse, view the results, and quickly transform them into a chart. The best part about using [!DNL SQL] to build reports is that you do not need to wait on update cycles to iterate on columns you create. If the results do not look right, you can quickly edit and rerun the query until things match your expectations.

This topic walks you through using the [!DNL SQL Report Builder]. After you know your way around, check out the [!DNL SQL] for visualizations tutorial or try optimizing some of the queries you have written.

Covered in this article:

1. [Writing a query](#writing)

1. [Running the query and viewing results](#runquery)

1. [Creating a visualization](#createviz)

1. [Saving the report](#save)

## [!DNL SQL Report Builder] Integrations

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) is the only integration unavailable for use with the [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). This functionality is in development.

To get started creating a [!DNL SQL] report, click **[!UICONTROL Report Builder]** or **[!UICONTROL Add Report]** at the top of any dashboard. In the [!DNL Report Picker] screen, click **[!UICONTROL SQL Report Builder]** to open the [!DNL SQL] editor.

## Get Started

To edit a report, click the gear (![](../../assets/gear-icon.png)) icon in the top-right corner of a [!DNL SQL]-based chart and click **[!UICONTROL Edit]**.

## Writing a query {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] queries are case-sensitive. Make sure you are using the correct case when writing queries or you could wind up with unexpected results or errors.

Following the [guidelines for query optimization](../../best-practices/optimizing-your-sql-queries.md), write a query in the [!DNL SQL] editor.

>[!IMPORTANT]
>
>**Metrics in [!DNL SQL] reports** - When you insert a metric into a SQL report, the `current definition` of the metric is used.

If the metric is updated in the future, the SQL report *does not* reflect the changes. You must manually edit the report to have the changes take effect.

Using the buttons at the top of the sidebar, you can toggle between lists of tables and metrics available for use in the [!DNL SQL Report Builder]. If you do not see what you are looking for in the list, try searching for it using the search bar at the top of the sidebar.

You can also use the sidebar in the [!DNL SQL] editor to insert metrics, tables, and columns directly into your queries by hovering over them and clicking **[!UICONTROL Insert]**:

![Inserting a table into the [!DNL SQL] editor.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Any [SELECT function](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), or any function that does not mutate data, that is supported by PostgreSQL is supported in the SQL Report Builder. This includes, but is not limited to, AVG, COUNT, COUNT DISTINCT, MIN/MAX, and SUM.

Also, any `JOIN` type is supported, but Adobe recommends only using INNER JOIN as it is the least expensive of the `JOIN` types.

## Running the query and viewing results {#runquery}

When you are done writing your query, click **[!UICONTROL Run Query]**. The results display in a table below the SQL editor:

![Running the query and viewing results.](../../assets/SQL_Run_Query.gif)

If something looks amiss in the results, you can edit the query and rerun it until you are satisfied.

You might sometimes see [messages below the editor with EXPLAIN in them](../../best-practices/optimizing-your-sql-queries.md). If you see one of these, that means that your query has not run and needs a bit of fine-tuning.

After you are done editing your query, you can move onto either creating a visualization or saving your work to a dashboard.

## Creating a visualization {#createviz}

To create a visualization with your query results, click the **[!UICONTROL Chart]** tab in the `Results` pane. In this tab, you select:

* The `Series`, or the column you want to measure, such as **Items sold**.
* The `Category`, or the column you want to use to segment your data, such as **acquisition source**.
* The `Labels`, or X-axis values.

Here is a quick look at what the visualization process looks like:

![](../../assets/SQL_RB_viz_overview.gif)

For a detailed walk-through of how to create a visualization, refer to the [Creating visualizations from SQL queries tutorial](../../tutorials/create-visuals-from-sql.md){: target="_blank"}.

## Saving the report {#save}

Before you can save your work, you must give the report a name. Remember to follow the [best practice guidelines for naming](../../best-practices/naming-elements.md){: target="_blank"} and choose something that clearly conveys what the report is!

Click **[!UICONTROL Save]** at the upper-right corner of the [!DNL SQL] editor and select the report `Type` (`Chart` or `Table`). To wrap things up, select the dashboard to save the report to and click **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analyze Your Data

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) gives you the power to directly query your Data Warehouse, view the results, and quickly transform them into a report. Using [!DNL SQL] also allows you [to use [!DNL SQL] functions that are not available](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) in the `Visual` or `Cohort` Report Builders, thus giving you greater control over your data.

Calculated columns created using [!DNL SQL] are not dependent on update cycles, meaning you can iterate on them as you please and immediately see results.

>[!NOTE]
>
>This only applies to the structure of the column, not the freshness of the data. Fresh data is still dependent on successfully completed update cycles.

|**This is perfect for...**|**This is not so great for...**|
|---|---|
|Intermediate/advanced analysts|Beginners - you need to know [!DNL SQL].|
|The [!DNL SQL] savvy|Simple analyses - writing a query can be more work than simply using the [!UICONTROL Visual Report Builder].|
|Building one-time-use calculated columns|Sharing with others - consider your audience: do they understand [!DNL SQL]? If not, they may be confused by how the report is built.|
|Data with `one-to-many` relationships||
|Testing a new column or analysis||

#### Database vs SQL Editor Results

Most the time, differences in results can be attributed to update cycles. If [!DNL Commerce Intelligence] is in the process of replicating data from your database to your Data Warehouse, you might see different results even when using the same query.

Connection issues can also result in discrepancies. Navigate to the `Connections` page by clicking **[!DNL Manage Data** > **Connections]** to check it out - is there an error for the database integration in question? If so, you may need to [reauthenticate the integration](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) to get things running again.

If all your integrations are connected successfully and you are not in the middle of an update cycle, something else may be amiss. 

#### Does deleting a [!DNL SQL] report also delete the underlying columns from my Data Warehouse?

No, you do not lose any columns from your Data Warehouse, regardless of how you built them.

Columns created using the `Data Warehouse Manager` are not affected if you delete a report or query that uses them.

Columns created using the [!DNL SQL Report Builder] are not saved to your Data Warehouse.


#### `Report Builder` versus `SQL Report Builder`

The [!DNL SQL Report Builder] gives you more flexibility when creating and structuring your charts - you can, for example, select what values should show on the `X` and `Y` axes. For more information on creating charts in the [!DNL SQL Report Builder], check out the [Creating visualizations from [!DNL SQL] queries](../../tutorials/create-visuals-from-sql.md) tutorial.

#### `Cohort Report Builder` {#cohortrb}

Unlike the [!DNL Visual Report Builder], the [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) is meant for a single purpose - analyzing and identifying behavioral trends of similar user groups over time. Using the [!DNL Cohort Report Builder] does not require any [!DNL SQL] savvy, so you can dive right in without hesitation if you are just starting out.

|**This is perfect for...**|**This is not so great for...**|
|---|---|
|Intermediate/advanced analysts|Beginners - you need practice-defining cohorts.|
|Identifying behavioral trends over time|Qualitative analysis - it can be [done](../dev-reports/create-qual-cohort-analysis.md), but requires Adobe assistance.|

## Rebuilding Queries after the Update Cycle

You do not have to rebuild your queries. Reports created using the [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) are saved like those created in the traditional `Report Builder`. The update process for [!DNL SQL] charts is the same - after your data is updated, the values in your charts will be recalculated and redisplayed.

>[!NOTE]
>
>When deleting a [!DNL SQL] report/query, it does not delete the underlying columns from your Data Warehouse. You do not lose any columns, regardless of how you built them.

* Columns created using the Data Warehouse Manager are not affected if you delete a report or query that uses them.

* Columns created using the SQL Report Builder are not saved to your Data Warehouse.

## Wrapping up {#wrapup}

If you want to try something a bit more challenging, why not try writing a query that is optimized for visualization? Check out the [Creating visualizations from [!DNL SQL] queries tutorial](../../tutorials/create-visuals-from-sql.md){: target="_blank"} to get started.
