---
title: Create and Use Data Warehouse Views
description: Learn about a method of creating new warehoused tables by modifying an existing table, or joining or consolidating multiple tables together through the use of SQL.
---
# Working with Data Warehouse Views

This document outlines the purpose and uses of _Data Warehouse Views_ accessible by navigating to **Manage Data** > **Data Warehouse Views**. Below is an explanation of what it does and how to create new views, as well as an example of how to use _Data Warehouse Views_ to consolidate Facebook and AdWords spend data.

## General Purpose

The _Data Warehouse Views_ feature is a method of creating new warehoused tables by modifying an existing table, or joining or consolidating multiple tables together through the use of SQL. Once a Data Warehouse View has been created and processed by an update cycle, it will populate in your Data Warehouse as a new table under the _Data Warehouse Views_ dropdown, as shown below:

![](../../assets/Data_Warehouse.png)

From here, your new view functions like any other table, giving you the power to create new calculated columns or build metrics and reports on top of it.

_Data Warehouse Views_ are primarily used to consolidate multiple similar but disparate tables together, such that all reporting can be built on a single new table. A few common examples include consolidating the tables from a legacy database and a live database to combine historical and current data, or combining multiple ad sources like Facebook and AdWords into a singular **Consolidated ad spend** table.

If you are familiar with SQL, both of these consolidation examples utilize the UNION function, but you can use any PostgreSQL syntax and functions when building a new view.

## Creating and Managing Data Warehouse Views

New _Data Warehouse Views_ can be created and existing views can be deleted by navigating to **Manage Data** > **Data Warehouse Views**, as shown below:

![](../../assets/Data_Warehouse_Views.png)

From here you can create a new view by following the sample instructions below:

1. If observing an existing view, click **New Data Warehouse View** to open a blank query window. If a blank query window is already open, proceed to the next step.
1. Give the view a name by typing in the **View Name** field. The name provided here will determine the display name for the view in the Data Warehouse. **View names are limited to lower case letters, numbers, and underscores (_).** All other characters are forbidden.
1. Enter your query in the window titled **Select Query**, using standard PostgreSQL syntax. Note that your query must reference specific column names. **The use of the * character to select all columns is not permitted.**
1. When you are finished, click **Save** to save your view. Note that your view will temporarily have a **Pending** status until it is processed by the next full update cycle, at which point the status will change to **Active**. After being processed by an update, your view is ready to use in reports.

It is important to mention that after saving, the underlying query used to generate a Data Warehouse View cannot be edited. If for some reason you need to adjust the structure of a Data Warehouse View, you will need to create a new view and manually migrate any calculated columns, metrics, or reports from the original view to the new one. When migration is complete, you can safely delete the original view. Because _Data Warehouse Views_ are not editable, we strongly recommend that you test the output of your query using the SQL Report Builder before saving your query as a Data Warehouse View.

## Example: Facebook and Google AdWords data

Let us take a look a closer look at one of the examples mentioned earlier in this article: consolidating Facebook and AdWords spend data into a new consolidated ads table. Most commonly this involves the consolidation of two tables, with sample data sets below:

**Ad source: Google AdWords**

**Table name: campaigns67890**

**Sample data:**

|**_id**|****campaign**|**adClicks**|**date**|**impressions**|**adCost**|
|--- |--- |--- |--- |--- |--- |
|1|eee|60|2017-05-05 00:00:00|2000|10.2|
|2|ggg|40|2017-05-23 00:00:00|900|4.6|
|3|aaa|22|2017-06-12 00:00:00|400|2.5|
|4|eee|350|2017-06-30 00:00:00|14500|35|
|5|fff|280|2017-07-10 00:00:00|10200|28.5|

**Ad source: Facebook**

**Table name: facebook_ads_insights_12345**

**Sample data:**

|**_id**|****campaign**|**adClicks**|**date**|**impressions**|**adCost**|
|--- |--- |--- |--- |--- |--- |
|1|aaa|25|2017-05-01 00:00:00|1200|5|
|2|ddd|12|2017-05-15 00:00:00|800|2.5|
|3|aaa|40|2017-05-22 00:00:00|2000|7|
|4|aaa|110|2017-06-08 00:00:00|6000|10|
|5|ccc|5|2017-07-06 00:00:00|300|1.2|

To create a single ad spend table containing both Facebook and AdWords campaigns, we will need to write a SQL query and make use of the UNION ALL function. A UNION ALL statement is most often used to combine multiple distinct SQL queries while appending the results of each query to a single output.

There are a few requirements of a UNION statement worth mentioning, as outlined in the PostgreSQL [documentation](https://www.postgresql.org/docs/8.3/queries-union.html):

* All queries must return the same number of columns
* Corresponding columns must have identical data types

When executing a UNION or UNION ALL statement, the names of the columns in the final output reflect the naming of columns in your first query.

In most cases, consolidating your Facebook and Google AdWords spend data into a Data Warehouse View will require the creation of a table with seven columns, with a query similar to the below:

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

A couple of important points about the above:

* For the sake of clarity, all columns are aliased above such that the names match across all queries. However this is not a requirement. The order in which columns are called in the SELECT queries dictates how they are lined up.
* A new column called **ad_source** is created to make it easier to filter for AdWords or Facebook data. Remember that this query combines all data from both tables. If you do not create a column like **ad_source**, there will be no easy way to identify spend from a particular source.

Saving the query above as a Data Warehouse View will create a new table with both Facebook and AdWords spend, similar to the below:

|**id**|**ad_source**|**date**|**campaign**|**spend**|**impressions**|**clicks**|
|--- |--- |--- |--- |--- |--- |--- |
|**1**|Facebook|2017-05-01 00:00:00|aaa|5|1200|25|
|**1**|AdWords|2017-05-05 00:00:00|eee|10.2|2000|60|
|**2**|Facebook|2017-05-15 00:00:00|ddd|2.5|800|12|
|**2**|AdWords|2017-05-23 00:00:00|ggg|4.6|900|40|
|**3**|Facebook|2017-05-22 00:00:00|aaa|7|2000|40|
|**3**|AdWords|2017-06-12 00:00:00|aaa|2.5|400|22|
|**4**|Facebook|2017-06-08 00:00:00|aaa|10|6000|110|
|**4**|AdWords|2017-06-30 00:00:00|eee|35|14500|350|
|**5**|Facebook|2017-07-06 00:00:00|ccc|1.2|300|5|
|**5**|AdWords|2017-07-10 00:00:00|fff|28.5|10200|280|

Rather than creating a separate set of marketing metrics for each ad source, you can now create just a single set of metrics using the table above to capture all of your ads.

**Looking for additional help?**

Writing SQL and creating Data Warehouse Views is not included with Technical Support.  However, the Services team does offer assistance in the creation of views. For everything from the migration and consolidation of a legacy database with a new database to the creation of a single Data Warehouse View for the purposes of a specific analysis, they are adept at curating SQL-based solutions for all of your data structure challenges.

In most cases, the creation of a new Data Warehouse View for the purposes of consolidating 2-3 similarly structured tables requires 5 hours of Services time, which translates to roughly $1250 of work. However below are a few common factors which can increase the expected investment required:

* Consolidation of more than 3 tables into a single view
* Creation of more than one data warehouse view
* Complex joining logic or filtering conditions
* Consolidation of 2 or more tables with dissimilar data structures
