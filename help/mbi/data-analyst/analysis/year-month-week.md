---
title: Yearly, Monthly, and Weekly Reports
description: Learn how to easily see trends over time and change perspective for time periods you may want to compare. 
---
# Reporting over Time Periods

>[!NOTE]
>
>This article contains instructions for clients that are utilizing the original architecture and new architecture. You are on the [new architecture](../../administrator/account-management/new-architecture.md) if you have the _Data Warehouse Views_ section available after selecting _Manage Data_ from the main toolbar.

The report builder allows you to easily see trends over time and change perspective for time periods you may want to compare. In this article, we will demonstrate how to set up a dashboard to go a level deeper to allow you to create reports for week over week, month over month and year over year analysis.

![](../../assets/Wow__mom__yoy.png)

Before getting started, you want to familiarize yourself with explore perspectives in more detail [here](../../tutorials/using-visual-report-builder.md) as well as independent time options [here](../../tutorials/time-options-visual-rpt-bldr.md).

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Calculated Columns

* **`Sales_flat_order`** table
* **Original architecture:** the below columns will be created by an analyst as part of your **[YoY WoW MoM ANALYSIS]** ticket
* **`created_at (month-day)`**
* **`created_at (month)`**
* **`created_at (day of the month)`**
* **`created_at (day of the week)`**
* **`created_at (hour of the day)`**

* **New architecture:** SQL listed below with a photo of an example for how to create this calculation
  * **`created_at (month-day)`** Calculation: **to_char(A, 'mm-dd')**
  * **`created_at (month)`** Calculation: **to_char(A, 'mm-month')**
  * **`created_at (day of the month)`**< Calculation: **to_char(A, 'dd')**
  * **`created_at (day of the week)`** Calculation: **to_char(A, 'd-Day')**
  * **`created_at (hour of the day)`** Calculation: **to_char(A, 'hh24')**
    ![](../../assets/Screen_Shot_2017-10-05_at_4.27.32_PM.png)

## Metrics

None.

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **YoY chart**
  * Metric: Number of orders

  * Metric: Number of orders
  * Time options: Time range (Custom): 2 years ago to 1 year ago

  * *Show top/bottom: Top 100% sorted by **`created_at (month-day)`***

* *Metric A: This year*
* *Metric B: Last year*
* *Time period: 1 year ago to 0 years ago*
* *Interval: None*
* *Group by: **`created_at (month-day)`***
* *Chart Type: Line*

* **MoM chart**
  * Metric: Number of orders

  * Metric: Number of orders
  * Time options: Time range (Custom): 2 months ago to 1 month ago

  * *Show top/bottom: Top 100% sorted by **`created_at (day of month)`***

* *Metric A: This month*
* *Metric B: Last month*
* *Time period: 1 month ago to 0 months ago*
* *Interval: None*
* *Group by: **`created_at (day of month)`***
* *Chart Type: Line*

* **WoW chart**
  * Metric: Number of orders

  * Metric: Number of orders
  * Time options: Time range (Custom): 2 weekss ago to 1 week ago

  * *Show top/bottom: Top 100% sorted by **`created_at (day of week)`***

* *Metric A: This week*
* *Metric B: Last week*
* *Time period: 1 week ago to 0 weeks ago*
* *Interval: None*
* *Group by: **`created_at (day of week)`***
* *Chart Type: Line*

* **DoD chart**
  * Metric: Number of orders

  * Metric: Number of orders
  * Time options: Time range (Custom): 2 days ago to 1 day ago

  * *Show top/bottom: Top 100% sorted by **`created_at (hour of day)`***

* *Metric A: Today*
* *Metric B: Yesterday*
* *Time period: 1 day ago to 0 days ago*
* *Interval: None*
* *Group by: **`created_at (hour of day)`***
* *Chart Type: Line*

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the image at the top of this page.
