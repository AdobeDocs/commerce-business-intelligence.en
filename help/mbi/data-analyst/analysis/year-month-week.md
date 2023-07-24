---
title: Yearly, Monthly, and Weekly Reports
description: Learn how to easily see trends over time and change perspective for time periods you may want to compare.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Reports, Dashboards
---
# Reporting over Time Periods

>[!NOTE]
>
>This topic contains instructions for clients that are using the original architecture and new architecture. You are on the [new architecture](../../administrator/account-management/new-architecture.md) if you have the [!DNL _Data Warehouse Views_] section available after selecting [!DNL Manage Data] from the main toolbar.

The report builder allows you to easily see trends over time and change perspective for time periods you may want to compare. This topic demonstrates how to set up a dashboard to go a level deeper to allow you to create reports for week over week, month over month and year over year analysis.

![](../../assets/Wow__mom__yoy.png)

Before getting started, you should review explore perspectives in more detail [here](../../tutorials/using-visual-report-builder.md) and independent time options [here](../../tutorials/time-options-visual-rpt-bldr.md).

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Calculated Columns

* **`Sales_flat_order`** table
* **Original architecture:** the below columns are created by an analyst as part of your `[YoY WoW MoM ANALYSIS]` ticket
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **New architecture:** SQL listed below with a photo of an example for how to create this calculation
  * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, 'mm-dd')**
  * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, 'mm-month')**
  * `created_at (day of the month)`< [!UICONTROL Calculation]: **to_char(A, 'dd')**
  * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, 'd-Day')**
  * **`created_at (hour of the day)` [!UICONTROL Calculation]: **to_char(A, 'hh24')**
    ![](../../assets/new-arch-create-calc.png)

## Metrics

None.

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **YoY chart**
  * [!UICONTROL Metric]: `Number of orders`

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

  * [!UICONTROL Show top/bottom]: Top 100% sorted by **`created_at (month-day)`***

* Metric `A`: `This year`
* Metric `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* [!UICONTROL Chart Type]: `Line`

* **MoM chart**
  * [!UICONTROL Metric]: `Number of orders`

  * [!UICONTROL Metric]: `Number of orders`
  * Time options: `Time range (Custom)`: `2 months ago to 1 month ago`

  * Show top/bottom: Top 100% sorted by **`created_at (day of month)`***

* Metric `A`: This month*
* Metric `B`: Last month*
* [!UICONTROL Time period]: one month ago to 0 months ago
* [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* [!UICONTROL Chart Type]: Line

* **WoW chart**
  * [!UICONTROL Metric]: `Number of orders`

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

  * [!UICONTROL Show top/bottom]: Top 100% sorted by `created_at (day of week)`

* Metric `A`: `This week`
* Metric `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* [!UICONTROL Chart Type]: `Line`

* **DoD chart**
  * [!UICONTROL Metric]: `Number of orders`

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

  * [!UICONTROL Show top/bottom]: Top 100% sorted by `created_at (hour of day)`

* Metric `A`: `Today`
* Metric B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* [!UICONTROL Chart Type]: `Line`

After compiling all the reports, you can organize them on the dashboard as you desire. The result may look like the image at the top of this page.
