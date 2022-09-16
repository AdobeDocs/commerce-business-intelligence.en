---
title: Reporting on a retail calendar
zendesk_id: 360016729771
---

In this article, we demonstrate how to set up the structure to use a [4-5-4 retail calendar](https://nrf.com/resources/4-5-4-calendar) within your MBI account. The visual report builder provides incredibly flexible time ranges, intervals and independent settings. Our team is also able to help you change the start day of the week to align with your business preferences. However, all of these settings work with the traditional monthly calendar in place.

Because many of our customers alter their calendar to use retail or accounting dates, the below steps will illustrate how to work with your data and create reports using retail dates. Though the below instructions will reference the 4-5-4 Retail calendar, you can alter them for any specific calendar your team uses, whether it be financial or just a custom time frame.

Before getting started, you want to familiarize yourself with [the File Uploader](../data-analyst/importing-data/connecting-data/using-file-uploader.md) and ensure that you have elongated the csv file so that the dates cover all of your historical data as well as push the dates into the future.

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Getting Started

You can [download](https://docs.magento.com/downloads/mbi/454_calendar.csv) a CSV version of the 4-5-4 retail calendar for retail years 2014 through 2017. Note that you may need to adjust this file according to your internal retail calendar as well as extend the date range to support your historical and current time frame. After downloading the file, use the File Uploader to create a Retail Calendar table in your MBI data warehouse. If you are using an unaltered version of the 4-5-4 retail calendar, ensure that the structure and data types of the fields in this table match the following:

| Column Name | Column Datatype | Primary Key |
| --- | --- | --- |
| Date Retail | Date & Time | Yes |
| Year Retail | Whole Number | No |
| Quarter Retail | Whole Number | No |
| Month Number Retail | Whole Number | No |
| Week Retail | Whole Number | No |
| Month Name Retail | Text (Up to 255 Characters) | No |
| Week Number of Month Retail | Whole Number | No |

## Columns to Create

* **sales\_order** table
   * **\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)**
      * Column type – "Same table -&gt; Calculation"
      * Inputs – **created\_at**
      * Datatype – Datetime
      * Calculation - \` **case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end**\`

* **Retail calendar** file upload table
   * **Current date**
      * Column type – "Same table -&gt; Calculation"
      * Inputs – **Date Retail**
      * Datatype – Datetime
      * Calculation - \`**case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end**\`
         * Note: The 'now()' function above is specific to PostgreSQL. Although most MBI data warehouses are hosted on PostgreSQL, some may be hosted on Redshift. If the calculation above returns an error, you may need to use the Redshift function 'getdate()' instead of 'now()'.
    * **Current retail year** (Must be created by support analyst)
      * Column type – "Event Counter"
      * Local Key - **Current date**
      * Remote Key - **Retail calendar.Date Retail**
      * Operation - Max
      * Operation value - Year Retail
   * **Included in current retail year? (Yes/No)**
      * Column type – "Same table -&gt; Calculation"
      * Inputs –
         * A - **Year Retail**
         * B - **Current retail year**
      * Datatype – String
      * Calculation - \`**case when A is null or B is null then null when A = B then 'Yes' else 'No' end**\`
   * **Included in previous retail year? (Yes/No)**
      * Column type – "Same table -&gt; Calculation"
      * Inputs –
         * A - **Year Retail**
         * B - **Current retail year**
      * Datatype – String
      * Calculation - \`**case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end**\`

* **sales\_order** table
   * **Created\_at (retail year)**
      * Column type – "One to Many -&gt; JOINED\_COLUMN"
      * Path -
         * Many: sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)
         * One: Retail Calendar.Date Retail
      * Select table: **Retail Calendar**
      * Select column: **Year Retail**
   * **Created\_at (retail week)**
      * Column type – "One to Many -&gt; JOINED\_COLUMN"
      * Path -
         * Many: sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)
         * One: Retail Calendar.Date Retail
      * Select table: **Retail Calendar**
      * Select column: **Week Retail**
   * **Created\_at (retail month)**
      * Column type – "One to Many -&gt; JOINED\_COLUMN"
      * Path -
         * Many: sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)
         * One: Retail Calendar.Date Retail
      * Select table: **Retail Calendar**
      * Select column: **Month Number Retail**
   * **Include in previous retail year? (Yes/No)**
      * Column type – "One to Many -&gt; JOINED\_COLUMN"
      * Path -
         * Many: sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)
         * One: Retail Calendar.Date Retail
      * Select table: **Retail Calendar**
      * Select column: **Include in previous retail year? (Yes/No)**
   * **Include in current retail year? (Yes/No)**
      * Column type – "One to Many -&gt; JOINED\_COLUMN"
      * Path -
         * Many: sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)
         * One: Retail Calendar.Date Retail
      * Select table: **Retail Calendar**
      * Select column: **Include in current retail year? (Yes/No)**

## Metrics

Note: No new metrics are needed for this analysis. However, make sure to [add the new columns you built in the sales\_order table as dimensions](../data-warehouse-mgr/manage-data-dimensions-metrics.md) for all metrics on the sales\_order table before continuing to the reports.

## Reports

* **Weekly orders - retail calendar (YoY)**
   * Metric A: 2017
      * Metric: Number of orders
      * Filter:
         * Created\_at (retail Year) = 2017
   * Metric B: 2016
      * Metric: Number of orders
      * Filter:
         * Created\_at (retail Year) = 2016
   * Metric C: 2015
      * Metric: Number of orders
      * Filter:
         * Created\_at (retail Year) = 2015
   * Time period: All time
   * Interval: None
   * Group by: Created\_at (retail week)
   * Chart Type: Line
      * Turn off multiple Y-axes

* **Retail calendar overview (current retail year by month)**
   * Metric A: Revenue
      * Metric: Revenue
      * Filter:
         * Include current retail year? = Yes
   * Metric B: Orders
      * Metric: Number of orders
      * Filter:
         * Include current retail year? = Yes
   * Metric C: Avg order value
      * Metric: Avg order value
      * Filter:
         * Include current retail year? = Yes
   * Time period: All time
   * Interval: None
   * Group by: Created\_at (retail month)
   * Chart Type: Line

* **Retail calendar overview (previous retail year by month)**
   * Metric A: Revenue
      * Metric: Revenue
      * Filter:
         * Include previous retail year? = Yes
   * Metric B: Orders
      * Metric: Number of orders
      * Filter:
         * Include previous retail year? = Yes
   * Metric C: Avg order value
      * Metric: Avg order value
      * Filter:
         * Include previous retail year? = Yes
   * Time period: All time
   * Interval: None
   * Group by: Created\_at (retail month)
   * Chart Type: Line

## Next Steps

The above describes how to configure a retail calendar to be compatible with any metric built on your sales\_order table (i.e., "Revenue" and "Orders"), but you can also extend this to support the retail calendar for metrics built on any table. The only requirement is that this table has a valid datetime field that can be used to join to the Retail Calendar table.

So for example, to view customer level metrics on a 4-5-4 retail calendar, create a new "Same Table" calculation in the customer\_entity table, similar to '\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)' described above. You can then use this column to reproduce all of the "One to Many" JOINED\_COLUMN calculations (like "Created_at (retail year)" and "Include in previous retail year? (Yes/No)") by joining the customer\_entity table to the Retail Calendar table.

Do not forget to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.
