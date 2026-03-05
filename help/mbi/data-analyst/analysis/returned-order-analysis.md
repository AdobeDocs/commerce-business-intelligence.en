---
title: Analyzing Returned Orders
description: Learn how to set up a dashboard that provides a detailed analysis of your store's returns.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/vEHbYcJUPlGk2eZsKvak9nSYBqOVvnKNSYDEutHMt3g
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Returned Orders

This topic demonstrates how to set up a dashboard that provides a detailed analysis of your store's returns.

![Detailed returns dashboard showing return rates and reasons](../../assets/detailed-returns-dboard.png)

Before getting started, you must be an [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) customer and should make sure that your company is using the `enterprise\_rma` table for returns.

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Getting Started

Columns to track

* **`enterprise_rma`** or **`rma`** table
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** or **`rma_item_entity`** table
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Filter sets to create

* **`enterprise_rma`** table
* Filter set name: `Returns we count`
* Filter set logic:
  * Placeholder - enter your custom logic here

* **`enterprise_rma_item_entity`** table
* Filter set name: `Returns items we count`
* Filter set logic:
  * Placeholder - enter your custom logic here

### Calculated Columns

Columns to create

* **`enterprise_rma`** table
* **`Order's created at`**
* Select a definition: `Joined Column`
* [!UICONTROL Create Path]:
* [!UICONTROL Many]: `enterprise_rma.order_id`
* [!UICONTROL One]: `sales_flat_order.entity_id`

* Select a [!UICONTROL table]: `sales_flat_order`
* Select a [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Select a definition: `Joined Column`
* Select a [!UICONTROL table]: `sales_flat_order`
* Select a [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** is created by an analyst as part of your `[RETURNS ANALYSIS]` ticket

* **`enterprise_rma_item_entity`** table
* **`return_date_requested`**
* Select a definition: `Joined Column`
* [!UICONTROL Create Path]:
  * [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
  * [!UICONTROL One]: `enterprise_rma.entity_id`

* Select a [!UICONTROL table]: `enterprise_rma`
* Select a [!UICONTROL column]: `date_requested`
  * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** is created by an analyst as part of your `[RETURNS ANALYSIS]` ticket

* **`sales_flat_order`** table
* **`Order contains a return? (1=yes/0=No)`**
* Select a definition: `Exists`
* Select a [!UICONTROL table]: `enterprise_rma`
  * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** is created by an analyst as part of your `[RETURNS ANALYSIS]` ticket
* **`Customer's previous order contains return? (1=yes/0=no)`** is created by an analyst as part of your `[RETURNS ANALYSIS]` ticket

>[!NOTE]
>
>If you are interested in analyzing only business hours for Seconds to resolution or Seconds to first response, let the analyst know when requesting the ticket.

### Metrics

* **Returns**
* In the **`enterprise_rma`** table
* This metric performs a **Count**
* On the **`entity_id`** column
* Ordered by the **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Returned items**
* In the **`enterprise_rma_item_entity`** table
* This metric performs a **Sum**
* On the **`qty_approved`** column
* Ordered by the **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Returned item total value**
* In the **`enterprise_rma_item_entity`** table
* This metric performs a **Sum**
* On the **`Returned item total value (qty_returned * price)`** column
* Ordered by the **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Average time between order and return**
* In the **`enterprise_rma`** table
* This metric performs an **Average**
* On the **`Time between order's created_at and date_requested`** column
* Ordered by the **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

### Reports

* **Repeat order probability after making a return**
* Metric `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* Metric `B`: `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* Formula: Repeat order probability
* [!UICONTROL Formula]: `B / A`
* [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart Type]: `Bar`

* **Avg time to return (all time)**
* Metric `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Number`

* **Percent of orders with a return**
* Metric `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Metric `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
  * `Order contains a return? (1=yes/0=No) = 1`

* Formula: % of orders with return
* [!UICONTROL Formula]: `B / A`
* [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Revenue returned by month**
* Metric `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* [!UICONTROL Chart Type]: `Line`

* **Customers who have made a return and not purchased again**
* Metric `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
    * `Order contains a return? (1=yes/0=No) = 1`
    * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer_email`
* [!UICONTROL Chart Type]: `Table`

* **Return rate by item**
* Metric `A`: `Returned items` (Hide)
* [!UICONTROL Metric]: Returned items

* Metric `B`: `Items sold` (Hide)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* [!UICONTROL Chart Type]: `Table`

After compiling all the reports, you can organize them on the dashboard as you desire. The result may look like the above sample dashboard.

If you run into any questions while building this analysis or want to engage the Professional Services team, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
