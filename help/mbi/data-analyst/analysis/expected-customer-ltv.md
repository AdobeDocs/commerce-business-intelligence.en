---
title: Expected Lifetime Value (LTV) Analysis for Pro
zendesk_id: 360016505552
---

In this article, we demonstrate how to set up a dashboard that will help you understand customer lifetime value growth and expected lifetime value of your customers.

![](../assets/upload_12_16_2016_at_3_03_34_PM.png)

This analysis is only available to Pro account customers on the new architecture. If your account has access to the Persistent Views feature under the Manage Data side bar, you are on the new architecture and can follow the instructions listed here to build this analysis yourself.

Before getting started, you will want to familiarize yourself with our [cohort report builder.](../data-analyst/dev-reports/cohort-rpt-bldr.md)

## Calculated Columns

Columns to create on the **orders** table if using **30-day months**:

* **Column name:** Months between first order and this order
* **Column type:** Same Table
* **Column equation:** CALCULATION
* **Column input:** A = `Seconds between customer’s first order date and this order`
* **Datatype:** Integer
* <strong>Definition: </strong>`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`
{: style="list-style-type: square;"}

* **Column name:** Months since order
* **Column type:** Same Table
* **Column equation:** CALCULATION
* **Column input:** A = `created_at`
* **Datatype:** Integer
* <strong>Definition: </strong>`case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`
{: style="list-style-type: square;"}
{: style="list-style-type: circle;"}
{: style="list-style-type: circle;"}

Columns to create on the **`orders`** table if using **calendar** months:

* **Column name:** Calendar months between first order and this order
* **Column type:** Same Table
* **Column equation:** CALCULATION
* **Column inputs:**
  * A = `created_at`
  * B = `Customer's first order date`
  {: style="list-style-type: square;"}

* **Datatype:** Integer
* <strong>Definition: </strong>`case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`
{: style="list-style-type: square;"}

* **Column name:** Calendar months since order
* **Column type:** Same Table
* **Column equation:** CALCULATION
* **Column input:** A = `created_at`
* **Datatype:** Integer
* <strong>Definition: </strong>`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`
{: style="list-style-type: square;"}

* **Column name:** Is in current month? (Yes/No)
* **Column type:** Same Table
* **Column equation:** CALCULATION
* **Column input:** A = `created_at`
* **Datatype:** String
* <strong>Definition: </strong>`case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`
{: style="list-style-type: square;"}
{: style="list-style-type: circle;"}
{: style="list-style-type: circle;"}

## Metrics

### Metric instructions

Metrics to create

* **Distinct customers by first order date***
  * If you enable guest orders, use <span class="wysiwyg-color-blue">**`customer_email`**</span>
  {: style="list-style-type: square;"}

* In the <span class="wysiwyg-color-blue">**`orders`**</span> table
* This metric performs a **Count Distinct Values**
* On the <span class="wysiwyg-color-blue">**`customer_id`**</span> column
* Ordered by the <span class="wysiwyg-color-blue">**`Customer's first order date`**</span> timestamp
{: style="list-style-type: circle;"}

Note: Make sure to [add all new columns as dimensions to metrics](../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

### Report instructions

**Expected revenue per customer by month**

* Metric A: Revenue (hide)
  * `Calendar months between first order and this order` &lt;= X (Pick some reasonable number for X, e.g. 24 months)
  * `Is in current month?` = No

* Metric: Revenue
* Filter:
{: style="list-style-type: square;"}

* Metric B: All time customers (hide)
  * `Is in current month?` = No

* Metric: New customers by first order date
* Filter:
{: style="list-style-type: square;"}

* Metric C: All time customers by month since first order (hide)
  * `Calendar months since order` &lt;= X
  * `Is in current month?` = No

* Metric: New customers by first order date
* Filter:
{: style="list-style-type: square;"}

* Formula: Expected revenue
* Formula: A / (B - C)
* Format: Currency
{: style="list-style-type: square;"}
{: style="list-style-type: circle;"}

Other chart details

* Time period: All time
* Time interval: None
* Group by: `Calendar months between first order and this order` - show all
* Change the goup by for the **All time customers** metric to Independent using the pencil icon next to the group by
* Edit the **Show top/bottom** fields as follows:
* **Revenue:** Top 24 sorted by Calendar months between first order and this order
* **All time customers:** Top 24 sorted by All time customers
* **All time customers by month since first order:** Top 24 sorted by All time customers by month since first order
{: style="list-style-type: square;"}
{: style="list-style-type: circle;"}

**Avg revenue per month by cohort**

* Metric A: Revenue
* Metric view: Cohort
* Cohort date: `Customer's first order date`
* Perspective: Average value per cohort member
{: style="list-style-type: square;"}
{: style="list-style-type: circle;"}

**Cumulative avg revenue per month by cohort**

* Metric A: Revenue
* Metric view: Cohort
* Cohort date: `Customer's first order date`
* Perspective: Cumulative average value per cohort member
{: style="list-style-type: square;"}
{: style="list-style-type: circle;"}

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the image at the top of the page.

If you run into any questions while building this analysis, or simply want to engage our professional services team, [contact support](https://support.magento.com/hc/en-us/articles/360016503692).
