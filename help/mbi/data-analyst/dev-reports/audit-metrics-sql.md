---
title: Working with SQL Report Builder
description: Learn how to audit data and metrics using the SQL Report Builder so that you can compare the results with the data from your local database.
---
# SQL Report Builder

The SQL Report Builder is primarily used to build new reports and iterate on analyses, but it can also be used to effectively audit data and metrics. The following information explains how to audit data and metrics using the SQL Report Builder so that you can compare the results with the data from your local database.

## Querying a metric

To get started, open the SQL Report Builder by navigating to **Report Builder > SQL Report Builder > Create Report**. You can use the sidebar in the SQL editor to insert a metric directly into your query by hovering over the metric and clicking **Insert**. This will add the query definition of that metric to the editor. The definition will include the following components:

-  The **metric operation** being performed, indicated by SUM() in the example below.
-  The **table on** which the metric is built, indicated by the FROM clause.
-  Any **filters (and filter sets)** that have been added to the metric, indicated by the WHERE clause in the example below.
-  The component of the **timestamp** (year, month) on which the data is to be ordered, indicated by the ORDER BY clause in the example below.

If you would like to have a clearer view of the query, you can reformat how it is displayed in the query field. When you are ready, select **Run Query**. The results will populate as a table in the report panel below the query.

![](../../mbi/assets//gif1.gif)

## Restricting the query

If you are trying to pinpoint a specific discrepancy or set of data, you should restrict the query to a specific sample to check against your local database. You can do this by editing the query to match your desired restrictions. In the following example, we are restricting the query to include only revenue from January 1, 2013 or later. After you update the query, select **Run Query** again to update the results.

![](../../mbi/assets//gif2.gif)

## Saving and exporting

When the report meets your needs, save it to a dashboard by giving the report a distinct name, clicking **Save**, and selecting the type of report you would like to save and the dashboard. When auditing metrics, we recommend saving the report as a **Table** and saving it to a test dashboard.

After the report is saved, navigate to that dashboard by selecting **Go to Dashboard**. From there, you can export the data by finding the report and selecting **Options gear > Full CSV Export** or **Full Excel Export.**

![](../../mbi/assets//gif3.gif)

## Custom queries

You can also write custom queries and export the results to compare against your local database. Following the [guidelines for query optimization](../../best-practices/optimizing-your-sql-queries.md), write a query in the SQL editor. You can use the buttons at the top of the sidebar to toggle between lists of tables and metrics available for use in the SQL Report Builder and add them to your query. When your custom query fits your needs, you can save the report and export that data from the dashboard.

### Still stumped?

If you find a discrepancy after auditing your data, take a look at the [Contacting Support: Data Discrepancies](https://support.magento.com/hc/en-us/articles/360016505312) support article for more information on what to do next.
