---
title: Translating SQL queries into[!DNL MBI]reports
description: Learn how SQL queries are translated into the calculated columns, metrics you use in MBI.
---
# Translate SQL queries in MBI

Ever wondered how SQL queries are translated into the [calculated columns](../data-warehouse-mgr/creating-calculated-columns.md), [metrics](../../data-user/reports/ess-manage-data-metrics.md), and [reports](../../tutorials/using-visual-report-builder.md) you use in MBI? If you are a heavy SQL user, understanding how SQL is translated in[!DNL MBI]will enable you to work smarter in the [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) and get the most out of the[!DNL MBI]platform.

At the end of this article, we have included a **translation matrix** for SQL query clauses and[!DNL MBI]elements.

We start by looking at a general query:

| | |
|--- |--- |
|`SELECT`||
|`a,`|Report group by|
|`SUM(b)`|Aggregate function(column)|
|`FROM c`|Source table|
|`WHERE`||
|`d IS NOT NULL`|Filter|
|`AND time < X`<br><br> `AND time >= Y`|Report time frame|
|`GROUP BY a`|Report group by|

This example covers the majority of translation cases, but there are some exceptions. Let us dive in, starting with how the aggregate function is translated.

## Aggregate functions

Aggregate functions (i.e., count, sum, average, max, min, etc) in queries either take the form of **metric aggregations** or **column aggregations** in MBI. The differentiating factor is whether or not a join is required to perform the aggregation.

Let us take a look at an example for each of the above.

## Metric aggregations {#aggregate}

A metric is required when aggregating _within a single table_. So for example, the SUM(b) aggregate function from the query above would most likely be represented by a metric which sums column "b". 

Let us look at a specific example of how a "Total Revenue" metric might be defined in MBI. Take a look at the query below that we will attempt to translate:

| | |
|--- |--- |
|`SELECT`||
|`SUM(order_total) as "Total Revenue"`|Metric operation(column)|
|`FROM orders|`Metric source table|
|`WHERE`||
|`email NOT LIKE '%@magento.com'`|Metric filter|
|`AND created_at < X`<br><br>`AND created_at >= Y`|Metric timestamp (and reporting time range)|

Navigating to the metric builder (**Manage Data **\=> **Metrics **\=> **Create New Metric**), we first must select the appropriate source table, which in this case is the "orders" table. Then the metric would be set up as shown below:

![Metric aggregation](../../assets/Metric_aggregation.png)

## Column aggregations

A calculated column is required when aggregating a column that is joined from another table. So for example, you may have a column built in your "customer" table called "Customer LTV", which sums the total value of all orders associated with that customer in the "orders" table.

The query for this aggregation may look something like the below:

|||
|--- |--- |
|`Select`| |
|`c.customer_id`|Aggregate owner|
|`SUM(o.order_total) as "Customer LTV"`|Aggregate operation(column)|
|`FROM customers c`|Aggregate owner table|
|`JOIN orders o`|Aggregation source table|
|`ON c.customer_id = o.customer_id`|Path|
|`WHERE o.status = 'success'`|Aggregate filter|

Setting this up in[!DNL MBI]requires the use of your **Data Warehouse** manager, where you will build a path between your "orders" and "customers" table then create a new column called "Customer LTV" in your customer's table.

Let us first take a look at how to establish a new path between the "customers" and "orders". Our end goal is to create a new aggregated column in the "customers" table, so first navigate to the "customers" table in your **Data Warehouse**, then click **Create a Column** \=> **Select a definition** => **SUM**.

Next, you need to select the source table. If a path already exists to your "orders" table, simply select it from the drop-down. However if you are building a new path, click **Create new path** and you will be presented with the screen below:

![Create new path](../../assets/Create_new_path.png)

Here you need to carefully consider the relationship between the two tables you are attempting to join together. In this case, there are potentially **Many** orders associated with **One** customer, therefore the "orders" table is listed on the **Many** side, whereas the "customers" table selected on the **One** side. Note that in MBI, a **path** is equivalent to a **Join** in SQL.

Once the path has been saved, you are all set to create the new "Customer LTV" column! Take a look at the below:

![](../../assets/Customer_LTV.gif)

Now that you have built the new "Customer LTV" column in your "customers" table, you are ready to create a [metric aggregation](#aggregate) utilizing this column (for example to find the average LTV per customer), or simply group by or filter by the calculated column in a report using existing metrics built on the "customers" table. Note that for the latter, any time you build a new calculated column you will need to [add the dimension to existing metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before it will be available as a filter or group by.

For more information on creating calculated columns with your Data Warehouse manager, take a look at [this article](../data-warehouse-mgr/creating-calculated-columns.md).

## GROUP BY clauses

GROUP BY functions in queries are often represented in[!DNL MBI]as a column used to segment or filter a visual report. As an example, Let us revisit the "Total Revenue" query that we explored previously, but this time Let us segment the revenue by the 'coupon\_code' to gain a better understanding of which coupons are generating the most revenue.

First, we start with the query below:

| | |
|--- |--- |
|`SELECT coupon_code,`|Report group by|
|`SUM(order_total) as "Total Revenue"`|Metric operation(column)|
|`FROM orders`|Metric source table|
|`WHERE`||
|`email NOT LIKE '%@magento.com'`|Metric filter|
|`AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'`|Metric timestamp (and reporting time range)|
|`GROUP BY coupon_code`|Report group by|

>[!NOTE]
>
>The only difference from the query we started with before is the addition of the 'coupon\_code' as the group by._

Using the same "Total Revenue" metric that we created previously, we are now ready to create our report of revenue segmented by coupon code! Take a look at the gif below which shows how to set up this visual report looking at data from September to November:

![Revenue by coupon code](../../assets/Revenue_by_coupon_code.gif)

## Formulas

In some cases, a query may involve multiple aggregations in order to calculate the relationship between separate columns. For example, you could calculate the average order value in a query through one of two ways:

*   AVG('order\_total') OR
*   SUM('order\_total')/COUNT('order\_id')

The former method would involve the creation of a new metric which performs an average on the 'order\_total' column. However the latter method could be created directly in the report builder assuming you already have metrics set up to calculate the "Total Revenue" and "Number of orders".

Let us take a step back and look at the overall query for "Average order value":

| | |
|--- |--- |
|`SELECT`||
|`SUM(order_total) as "Total Revenue"`|Metric operation(column)|
|`COUNT(order_id) as "Number of orders"`|Metric operation(column)|
|`SUM(order_total)/COUNT(order_id) as "Average order value"`|Metric operation(column) / Metric operation(column)|
|`FROM orders`|Metric source table|
|`WHERE`||
|`email NOT LIKE '%@magento.com'`|Metric filter|
|`AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'`|Metric timestamp (and reporting time range)|

And Let us also assume we already have metrics set up to calculate the "Total Revenue" and "Number of orders". Since these metrics already exist, we can simply open the Report Builder and create an ad hoc calculation using the Formula feature:

![AOV forumula](../../assets/AOV_forumula.gif)

## Wrapping Up

As we mentioned at the beginning of this article, if you are a heavy SQL user, thinking about how queries translate in[!DNL MBI]will enable you to build calculated columns, metrics, and reports.

For quick reference, check out the matrix below. This shows a SQL clause's equivalent[!DNL MBI]element and how it can map to more than one element, depending on how it is used in the query.

## MBI Elements

|**SQL Clause**|**Metric**|**Filter**|**Report group by**|**Report time frame**|**Path**|**Calculated column inputs**|**Source table**|
|--|--|--|--|--|--|--|--|
|**SELECT**|X|-|X|-|-|X|-|
|**FROM**|-|-|-|-|-|-|X|
|**WHERE**|-|X|-|-|-|-|-|
|**WHERE (with time elements)**|-|-|-|X|-|-|-|
|**JOIN...ON**|-|X|-|-|X|X|-|
|**GROUP BY**|-|-|X|-|-|-|-|
