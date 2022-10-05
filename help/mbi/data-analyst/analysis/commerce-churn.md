---
title: Commerce Churn
description: Learn how to generate and analyze your Commerce churn rate. 
---
# Churn Rate

In this topic article, we demonstrate how to calculate a **churn rate** for your **commerce customers**. Unlike SaaS or traditional subscription companies, commerce customers typically do not have a concrete **"churn event"** to show you that they should no longer count toward your active customers. For this reason, the below instructions allow you to define a customer as "churned" based upon a determined amount of time passing since their last order.

![](../../mbi/assets/Churn_rate_image.png)

Many customers want assistance in starting to conceptualize what **timeframe** they should use based upon their data. If you want to use historical customer behavior to define this **churn timeframe**, you may want to familiarize yourself with the [defining churn](../analysis/define-cust-churn.md) Analysis Library article. Then, you can use the results in the formula for churn rate in the below instructions.

## Calculated Columns

Columns to create

* <!--<span class="wysiwyg-color-blue">-->**`customer_entity`**<!--</span>--> table
* <!--<span class="wysiwyg-color-blue">-->**`Customer's last order date`**<!--</span>-->
  * Select a definition: Max
  * Select table: <!--<span class="wysiwyg-color-blue">-->**`sales_flat_order`**<!--</span>-->
  * Select column: <!--<span class="wysiwyg-color-blue">-->**`created_at`**<!--</span>-->
  * sales_flat_order.customer_id = customer_entity.entity_id
  * Filter:
  * Orders we count
  <!--{: style="list-style-type: square;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`Seconds since customer's last order date`**<!--</span>-->
  * Select a definition: Age
  * Select column: <!--<span class="wysiwyg-color-blue">-->**`Customer's last order date`**<!--</span>--><!--<span class="wysiwyg-color-blue">-->**``**<!--</span>--><!--<span class="wysiwyg-color-blue">-->**``**<!--</span>-->
  <!--{: style="list-style-type: square;"}-->

Note: Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Metrics

* **New customers (by first order date)**
  * Customers we count
  <!--{: style="list-style-type: circle;"}-->

* NOTE: this metric may already exist on your account
* In the <!--<span class="wysiwyg-color-blue">-->**`customer_entity`**<!--</span>--> table
* This metric performs a **Count**
* On the <!--<span class="wysiwyg-color-blue">-->**`entity_id`**<!--</span>--> column
* Ordered by the <!--<span class="wysiwyg-color-blue">-->**`Customer's first order date`**<!--</span>--> timestamp
* Filter:
<!--{: style="list-style-type: circle;"}-->

* **New customers (by last order date)**
  * Customers we count
  <!--{: style="list-style-type: circle;"}-->

* **Note**: this metric may already exist on your account
* In the <!--<span class="wysiwyg-color-blue">-->**`customer_entity`**<!--</span>--> table
* This metric performs a **Count**
* On the <!--<span class="wysiwyg-color-blue">-->**`entity_id`**<!--</span>--> column
* Ordered by the <!--<span class="wysiwyg-color-blue">-->**`Customer's last order date`**<!--</span>--> timestamp
* Filter:
<!--{: style="list-style-type: circle;"}-->

Note: Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **Churn Rate**
  * Metric: New customers (by first order date)
  * Filter:
  * Lifetime number of orders Greater Than 0

  * Perspective: Cumulative
  <!--{: style="list-style-type: square;"}-->

  * Metric: New customers (by last order date)
  * Filter:
  * Seconds since customer's last order date >= [Your self-defined cutoff for churned customers]<!--<span class="wysiwyg-color-blue">-->**`^`**<!--</span>-->
  * Lifetime number of orders Greater Than 0
  <!--{: style="list-style-type: square;"}-->

  * Metric: New customers (by last order date)
  * Filter:
  * Lifetime number of orders Greater Than 0

  * Perspective: Cumulative
  <!--{: style="list-style-type: square;"}-->

  * Formula: (B / ((A + B) - C)
  * Format: Percentage
  <!--{: style="list-style-type: square;"}-->

* *Metric A: New customers cumulative*
* *Metric B: Churned customers by last order date*
* *Metric C: Customers by last order date cumulative*
* *Formula: Repeat order probability*
* *Time period: All time (or custom range)*
* *Group by: Customer's order number*
* *Chart Type: Column*
<!--{: style="list-style-type: circle;"}-->

Below are some common month > second conversions, but google provides other values, including week > seconds conversions for any custom values you may be looking for.

| **Months** | **Seconds** |
{: align="center"}| 3 | 7,776,000 |
{: align="center"}| 6 | 15,552,000 |
{: align="center"}| 9 | 23,328,000 |
{: align="center"}| 12 | 31,104,000 |
{: align="center"}{: align="center"}

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the above sample dashboard.
