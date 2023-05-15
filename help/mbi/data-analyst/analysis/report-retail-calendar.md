---
title: Reporting on a retail calendar
description: Learn how to set up the structure to use a 4-5-4 retail calendar within your [!DNL Commerce Intelligence] account.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
---
# Reporting on a Retail Calendar

This article demonstrates how to set up the structure to use a [4-5-4 retail calendar](https://nrf.com/resources/4-5-4-calendar) within your [!DNL Commerce Intelligence] account. The visual report builder provides incredibly flexible time ranges, intervals, and independent settings. However, all of these settings work with the traditional monthly calendar in place.

Because many customers alter their calendar to use retail or accounting dates, the below steps illustrate how to work with your data and create reports using retail dates. Though the below instructions reference the 4-5-4 Retail calendar, you can alter them for any specific calendar your team uses, whether it be financial or just a custom time frame.

Before getting started, you need to familiarize yourself with [the File Uploader](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) and ensure that you have elongated the `.csv` file. This ensures that the dates cover all of your historical data and push the dates into the future.

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Getting Started

You can [download](../../assets/454-calendar.csv) a `.csv` version of the 4-5-4 retail calendar for retail years 2014 through 2017. You may need to adjust this file according to your internal retail calendar and extend the date range to support your historical and current time frame. After downloading the file, use the File Uploader to create a Retail Calendar table in your [!DNL Commerce Intelligence] Data Warehouse. If you are using an unaltered version of the 4-5-4 retail calendar, ensure that the structure and data types of the fields in this table match the following:

| Column Name | Column Datatype | Primary Key |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Up to 255 Characters) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Columns to Create

* **sales\_order** table
   * `INPUT` `created\_at` (yyyy-mm-dd 00:00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Retail calendar** file upload table
   * **Current date**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * [!UICONTROL Datatype]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >The `now()` function above is specific to PostgreSQL. Although most [!DNL Commerce Intelligence] data warehouses are hosted on PostgreSQL, some may be hosted on Redshift. If the calculation above returns an error, you may need to use the Redshift function `getdate()` instead of `now()`.

    * **Current retail year** (Must be created by support analyst)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Included in current retail year? (Yes/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: 
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * [!UICONTROL Datatype]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Included in previous retail year? (Yes/No)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * [!UICONTROL Datatype]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* **sales\_order** table
   * **Created\_at (retail year)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Path -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Select a [!UICONTROL table]: `Retail Calendar`
      * Select a [!UICONTROL column]: `Year Retail`
   * **Created\_at (retail week)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Path -
         * [!UICONTROL Many]: sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00
         * [!UICONTROL One]: Retail Calendar.Date Retail
      * Select a [!UICONTROL table]: `Retail Calendar`
      * Select a [!UICONTROL column]: `Week Retail`
   * **Created\_at (retail month)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Path 
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Select a [!UICONTROL table]: `Retail Calendar`
      * Select a [!UICONTROL column]: `Month Number Retail`
   * **Include in previous retail year? (Yes/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Path -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Retail `Calendar.Date Retail`
      * Select a [!UICONTROL table]: `Retail Calendar`
      * Select a [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **Include in current retail year? (Yes/No)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Path -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Retail `Calendar.Date Retail`
      * Select a [!UICONTROL table]: `Retail Calendar`
      * Select a [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Metrics

Note: No new metrics are needed for this analysis. However, make sure to [add the new columns you built in the sales\_order table as dimensions](../data-warehouse-mgr/manage-data-dimensions-metrics.md) for all metrics on the sales\_order table before continuing to the reports.

## Reports

* **Weekly orders - retail calendar (YoY)**
   * Metric `A`: `2017`
      * [!UICONTROL Metric]: Number of orders
      * [!UICONTROL Filter]:
         * Created\_at (retail Year) = 2017
   * Metric `B`: `2016`
      * [!UICONTROL Metric]: Number of orders
      * [!UICONTROL Filter]:
         * Created\_at (retail Year) = 2016
   * Metric `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Created\_at` (retail week)
   * [!UICONTROL Chart type]: `Line`
      * Turn off `multiple Y-axes`

* **Retail calendar overview (current retail year by month)**
   * Metric `A`: `Revenue`
      * [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * [!UICONTROL Include current retail year? ]: `Yes`
   * Metric `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * [!UICONTROL Include current retail year? ]: `Yes`
   * Metric `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * [!UICONTROL Include current retail year? ]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Created\_at` (retail month)
   * [!UICONTROL Chart type]: `Line`

* **Retail calendar overview (previous retail year by month)**
   * Metric `A`: `Revenue`
      * [!UICONTROL Metric]: `Revenue`
      * [!UICONTROL Filter]:
         * [!UICONTROL Include current retail year? ]: `Yes`
   * Metric `B`: `Orders`
      * [!UICONTROL Metric]: Number of orders
      * [!UICONTROL Filter]:
         * [!UICONTROL Include current retail year? ]: `Yes`
   * Metric `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * [!UICONTROL Include current retail year? ]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `None`
   * [!UICONTROL Group by]: `Created\_at` (retail month)
   * [!UICONTROL Chart type]: `Line`

## Next Steps

The above describes how to configure a retail calendar to be compatible with any metric built on your `sales\_order` table (such as `Revenue` or `Orders`). You can also extend this to support the retail calendar for metrics built on any table. The only requirement is that this table has a valid datetime field that can be used to join to the Retail Calendar table.

So for example, to view customer level metrics on a 4-5-4 retail calendar, create a `Same Table` calculation in the `customer\_entity` table, similar to `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` described above. You can then use this column to reproduce the `One to Many` JOINED\_COLUMN calculations (like `Created_at (retail year)` and `Include in previous retail year? (Yes/No)` by joining the `customer\_entity` table to the `Retail Calendar` table.

Do not forget to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.
