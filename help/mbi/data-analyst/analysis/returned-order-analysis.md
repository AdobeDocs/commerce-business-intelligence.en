---
title: Analyzing Returned Orders
description: Learn how to set up a dashboard that will provide a detailed analysis of your store's returns. 
---
# Returned Orders

In this article, we demonstrate how to set up a dashboard that will provide a detailed analysis of your store's returns.

![](../../mbi/assets//upload_12_19_2016_at_3_34_09_PM.png)

Before getting started, you will need to be an [Enterprise client of Magento](https://magento.com/products/magento-commerce) and will want to make sure your company is using the `enterprise\_rma` table for returns.

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Getting Started

Columns to track

* <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma`**<!--</span>--> or <!--<span class="wysiwyg-color-blue">-->**`rma`**<!--</span>--> table
* <!--<span class="wysiwyg-color-blue">-->**`entity_id`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`status`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`order_id`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`customer_id`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`date_requested`**<!--</span>-->
<!--{: style="list-style-type: circle;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma_item_entity`**<!--</span>--> or <!--<span class="wysiwyg-color-blue">-->**`rma_item_entity`**<!--</span>--> table
* <!--<span class="wysiwyg-color-blue">-->**`entity_id`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`rma_entity_id`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`qty_returned`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`status`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`order_item_id`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`product_name`**<!--</span>-->
* <!--<span class="wysiwyg-color-blue">-->**`product_sku`**<!--</span>-->
<!--{: style="list-style-type: circle;"}-->

Filter sets to create

* <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma`**<!--</span>--> table
* Filter set name: Returns we count
* Filter set logic:
* Placeholder - enter your custom logic here
<!--{: style="list-style-type: circle;"}-->
<!--{: style="list-style-type: circle;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma_item_entity`**<!--</span>--> table
* Filter set name: Returns items we count
* Filter set logic:
* Placeholder - enter your custom logic here
<!--{: style="list-style-type: circle;"}-->
<!--{: style="list-style-type: circle;"}-->

### Calculated Columns

Columns to create

* <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma`**<!--</span>--> table
* <!--<span class="wysiwyg-color-blue">-->**`Order's created at`**<!--</span>-->
* Select a definition: Joined Column
* Create Path:
* Many: enterprise_rma.order_id
* One: sales_flat_order.entity_id

* Select table: <!--<span class="wysiwyg-color-blue">-->**`sales_flat_order`**<!--</span>-->
* Select column: <!--<span class="wysiwyg-color-blue">-->**`created_at`**<!--</span>-->
* enterprise_rma.order_id = sales_flat_order.entity_id
<!--{: style="list-style-type: square;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`Customer's order number`**
* Select a definition: Joined Column
* Select table: <!--<span class="wysiwyg-color-blue">-->**`sales_flat_order`**<!--</span>-->
* Select column: <!--<span class="wysiwyg-color-blue">-->**`Customer's order number`**<!--</span>-->
* enterprise_rma.order_id = sales_flat_order.entity_id
<!--{: style="list-style-type: square;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`Time between order's created_at and date_requested`**<!--</span>--> will be created by an analyst as part of your **[RETURNS ANALYSIS]** ticket
<!--{: style="list-style-type: circle;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma_item_entity`** table
* <!--<span class="wysiwyg-color-blue">-->**`return_date_requested`**
* Select a definition: Joined Column
* Create Path:
* Many: enterprise_rma_item_entity.rma_entity_id
* One: enterprise_rma.entity_id

* Select table: <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma`**<!--</span>-->
* Select column: <!--<span class="wysiwyg-color-blue">-->**`date_requested`**<!--</span>-->
* enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id
<!--{: style="list-style-type: square;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`Return item total value (qty_returned * price)`**<!--</span>--> will be created by an analyst as part of your **[RETURNS ANALYSIS]** ticket
<!--{: style="list-style-type: circle;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`sales_flat_order`** table
* <!--<span class="wysiwyg-color-blue">-->**`Order contains a return? (1=yes/0=No)`**
* Select a definition: Exists
* Select table: <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma`**<!--</span>-->
* enterprise_rma.order_id = sales_flat_order.entity_id
<!--{: style="list-style-type: square;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`Customer's previous order number`**<!--</span>--> will be created by an analyst as part of your **[RETURNS ANALYSIS]** ticket
* <!--<span class="wysiwyg-color-blue">-->**`Customer's previous order contains return? (1=yes/0=no)`**<!--</span>--> will be created by an analyst as part of your **[RETURNS ANALYSIS]** ticket
<!--{: style="list-style-type: circle;"}-->

<!--<span class="wysiwyg-color-blue">-->**`^`**<!--</span>--> If you are interested in analyzing only business hours for Seconds to resolution or Seconds to first response, let the analyst know when requesting the ticket.

### Metrics

* **Returns**
* In the <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma`**<!--</span>--> table
* This metric performs a **Count**
* On the <!--<span class="wysiwyg-color-blue">-->**`entity_id`**<!--</span>--> column
* Ordered by the <!--<span class="wysiwyg-color-blue">-->**`date_requested`**<!--</span>-->
* Filter:
* Returns we count
<!--{: style="list-style-type: square;"}-->
<!--{: style="list-style-type: circle;"}-->

* **Returned items**
* In the <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma_item_entity`**<!--</span>--> table
* This metric performs a **Sum**
* On the <!--<span class="wysiwyg-color-blue">-->**`qty_approved`**<!--</span>--> column
* Ordered by the <!--<span class="wysiwyg-color-blue">-->**`return date_requested`**<!--</span>-->
* Filter:
* Returns we count
<!--{: style="list-style-type: square;"}-->
<!--{: style="list-style-type: circle;"}-->

* **Returned item total value**
* In the <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma_item_entity`**<!--</span>--> table
* This metric performs a **Sum**
* On the <!--<span class="wysiwyg-color-blue">-->**`Returned item total value (qty_returned * price)`**<!--</span>--> column
* Ordered by the <!--<span class="wysiwyg-color-blue">-->**`return date_requested`**<!--</span>-->
* Filter:
* Returns we count
<!--{: style="list-style-type: square;"}-->
<!--{: style="list-style-type: circle;"}-->

* **Average time between order and return**
* In the <!--<span class="wysiwyg-color-blue">-->**`enterprise_rma`**<!--</span>--> table
* This metric performs a **Average**
* On the <!--<span class="wysiwyg-color-blue">-->**`Time between order's created_at and date_requested`**<!--</span>--> column
* Ordered by the <!--<span class="wysiwyg-color-blue">-->**`date_requested`**<!--</span>-->
* Filter:
* Returns we count
<!--{: style="list-style-type: square;"}-->
<!--{: style="list-style-type: circle;"}-->

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

### Reports

* **Repeat order probability after making a return**
* *Metric A: Number of orders with returns*
* Metric: Number of orders
* Filter:
* Order contains a return? (1=yes/0=No) = 1
* Is in current month? = No
<!--{: style="list-style-type: square;"}-->

* *Metric B: Non-last orders with returns*
* Metric: Number of orders
* Filter:
* Is customer's last order? (1=yes/0=no) = 0
* Order contains a return? (1=yes/0=No) = 1
<!--{: style="list-style-type: square;"}-->

* *Formula: Repeat order probability*
* Formula: B / A
* Format: Percentage
<!--{: style="list-style-type: square;"}-->

* *Time period: All time*
* *Interval: None*
* *Group by: Customer's order number*
* *Chart Type: Bar*
<!--{: style="list-style-type: circle;"}-->

* **Avg time to return (all time)**
* *Metric A: Avg time between order and return*
* Metric: Avg time between order and return
<!--{: style="list-style-type: square;"}-->

* *Time period: All time*
* *Interval: None*
* *Chart Type: Number*
<!--{: style="list-style-type: circle;"}-->

* **Percent of orders with a return**
* *Metric A: Number of orders*
* Metric: Number of orders
<!--{: style="list-style-type: square;"}-->

* *Metric B: Orders w/ return*
* Metric: Number of orders
* Filter:
* Order contains a return? (1=yes/0=No) = 1
<!--{: style="list-style-type: square;"}-->

* *Formula: % of orders with return*
* Formula: B / A
* Format: Percentage
<!--{: style="list-style-type: square;"}-->

* *Time period: All time*
* *Interval: None*
* *Chart Type: Number - % of orders with return*
<!--{: style="list-style-type: circle;"}-->

* **Revenue returned by month**
* *Metric A: Returned item total value*
* Metric: Returned item total value
<!--{: style="list-style-type: square;"}-->

* *Time period: All time*
* *Interval: By month*
* *Chart Type: Line*
<!--{: style="list-style-type: circle;"}-->

* **Customers who have made a return and not purchased again**
* *Metric A: Number of orders with returns*
* Metric: Number of orders
* Filter:
* Order contains a return? (1=yes/0=No) = 1
* Is customer's last order? (1=yes/0=no) = 1
<!--{: style="list-style-type: square;"}-->

* *Time period: All time*
* *Interval: None*
* *Group by: Customer_email*
* *Chart Type: table*
<!--{: style="list-style-type: circle;"}-->

* **Return rate by item**
* *Metric A: Returned items* (Hide)
* Metric: Returned items
<!--{: style="list-style-type: square;"}-->

* *Metric B: Items sold*(Hide)
* Metric: Number of orders
* Filter:
<!--{: style="list-style-type: square;"}-->

* *Formula: Return %*
* Formula: B / A
* Format: Percentage
<!--{: style="list-style-type: square;"}-->

* *Time period: All time*
* *Interval: None*
* *Group by: product_sku AND/OR product_name*
* *Chart Type: table*
<!--{: style="list-style-type: circle;"}-->

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the above sample dashboard.

If you run into any questions while building this analysis, or simply want to engage our professional services team, [contact support](../../getting-started/support.md).
