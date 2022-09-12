---
title: Year-over-year, month-over-month, week-over-week
zendesk_id: 360016506952
---

{: .bs-callout-info}
This article contains instructions for clients that are utilizing the original architecture and new architecture. You are on the [new architecture](../../administrator/account-management/new-architecture.md) if you have the "Data Warehouse Views" section available after selecting "Manage Data" from the main toolbar.

The report builder allows you to easily see trends over time and change perspective for time periods you may want to compare. In this article, we will demonstrate how to set up a dashboard to go a level deeper to allow you to create reports for week over week, month over month and year over year analysis.

![](../../assets/Wow__mom__yoy.png)

Before getting started, you want to familiarize yourself with explore perspectives in more detail [here](../../tutorials/using-visual-report-builder.md) as well as independent time options [here](../../tutorials/time-options-visual-rpt-bldr.md).

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

### Calculated Columns

* <span class="wysiwyg-color-blue">**`Sales_flat_order`**</span> table
* **Original architecture:** the below columns will be created by an analyst as part of your **[YoY WoW MoM ANALYSIS]** ticket
* <span class="wysiwyg-color-blue">**`created_at (month-day)`**</span>
* <span class="wysiwyg-color-blue">**`created_at (month)`**</span>
* <span class="wysiwyg-color-blue">**`created_at (day of the month)`**</span>
* <span class="wysiwyg-color-blue">**`created_at (day of the week)`**</span>
* <span class="wysiwyg-color-blue">**`created_at (hour of the day)`**</span>
{: style="list-style-type: circle;"}

* **New architecture:** SQL listed below with a photo of an example for how to create this calculation
  * <span class="wysiwyg-color-blue">**`created_at (month-day)`**</span> Calculation**:** **to_char(A, 'mm-dd')**
  * <span class="wysiwyg-color-blue">**`created_at (month)`**</span> Calculation**:** **to_char(A, 'mm-month')**
  * <span class="wysiwyg-color-blue">**`created_at (day of the month)`**</span> Calculation**:** **to_char(A, 'dd')**
  * <span class="wysiwyg-color-blue">**`created_at (day of the week)`**</span> Calculation**:** **to_char(A, 'd-Day')**
  * <span class="wysiwyg-color-blue">**`created_at (hour of the day)`**</span> Calculation**:** **to_char(A, 'hh24')**
    ![Screen\_Shot\_2017-10-05\_at\_4.27.32\_PM.png](../../assets/Screen_Shot_2017-10-05_at_4.27.32_PM.png)

### Metrics

None.

**Note:** Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

### Reports

* **YoY chart**
  * Metric: Number of orders
  {: style="list-style-type: square;"}

  * Metric: Number of orders
  * Time options: Time range (Custom): 2 years ago to 1 year ago
  {: style="list-style-type: square;"}

  * *Show top/bottom: Top 100% sorted by **`created_at (month-day)`***

* *Metric A: This year*
* *Metric B: Last year*
* *Time period: 1 year ago to 0 years ago*
* *Interval: None*
* *Group by: **`created_at (month-day)`***
* *Chart Type: Line*
{: style="list-style-type: circle;"}

* **MoM chart**
  * Metric: Number of orders
  {: style="list-style-type: square;"}

  * Metric: Number of orders
  * Time options: Time range (Custom): 2 months ago to 1 month ago
  {: style="list-style-type: square;"}

  * *Show top/bottom: Top 100% sorted by **`created_at (day of month)`***

* *Metric A: This month*
* *Metric B: Last month*
* *Time period: 1 month ago to 0 months ago*
* *Interval: None*
* *Group by: **`created_at (day of month)`***
* *Chart Type: Line*
{: style="list-style-type: circle;"}

* **WoW chart**
  * Metric: Number of orders
  {: style="list-style-type: square;"}

  * Metric: Number of orders
  * Time options: Time range (Custom): 2 weekss ago to 1 week ago
  {: style="list-style-type: square;"}

  * *Show top/bottom: Top 100% sorted by **`created_at (day of week)`***

* *Metric A: This week*
* *Metric B: Last week*
* *Time period: 1 week ago to 0 weeks ago*
* *Interval: None*
* *Group by: **`created_at (day of week)`***
* *Chart Type: Line*
{: style="list-style-type: circle;"}

* **DoD chart**
  * Metric: Number of orders
  {: style="list-style-type: square;"}

  * Metric: Number of orders
  * Time options: Time range (Custom): 2 days ago to 1 day ago
  {: style="list-style-type: square;"}

  * *Show top/bottom: Top 100% sorted by **`created_at (hour of day)`***

* *Metric A: Today*
* *Metric B: Yesterday*
* *Time period: 1 day ago to 0 days ago*
* *Interval: None*
* *Group by: **`created_at (hour of day)`***
* *Chart Type: Line*
{: style="list-style-type: circle;"}

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the image at the top of this page.
