---
title: Commerce Churn
description: Learn how to generate and analyze your Commerce churn rate.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/jtS4f7MMpKa8LrKDOvGOqNJfrl-MhR9vhEMQZa-B42o
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
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Churn Rate

This topic demonstrates how to calculate a **churn rate** for your **commerce customers**. Unlike SaaS or traditional subscription companies, commerce customers typically do not have a concrete **"churn event"** to show you that they should no longer count toward your active customers. For this reason, the below instructions allow you to define a customer as "churned" based on a determined amount of time passing since their last order.

![Churn rate visualization showing customer retention over time](../../assets/Churn_rate_image.png)

Many customers want assistance in starting to conceptualize what **timeframe** they should use based on their data. If you want to use historical customer behavior to define this **churn timeframe**, you may want to familiarize yourself with the [defining churn](../analysis/define-cust-churn.md) topic. Then, you can use the results in the formula for churn rate in the below instructions.

## Calculated Columns

Columns to create

* **`customer_entity`** table
* **`Customer's last order date`**
  * Select a [!UICONTROL definition]: `Max`
  * Select [!UICONTROL table]: `sales_flat_order`
  * Select [!UICONTROL column]: `created_at`
  * `sales_flat_order.customer_id = customer_entity.entity_id`
  * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
  * Select a [!UICONTROL definition]: `Age`
  * Select [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Metrics

* **New customers (by first order date)**
  * Customers that are counted

>[!NOTE]
>
>This metric may exist on your account.

* In the **`customer_entity`** table
* This metric performs a **Count**
* On the **`entity_id`** column
* Ordered by the **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **New customers (by last order date)**
  * Customers that are counted

   >[!NOTE]
   >
   >This metric may exist on your account.

* In the **`customer_entity`** table
* This metric performs a **Count**
* On the **`entity_id`** column
* Ordered by the **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **Churn Rate**
  * [!UICONTROL Metric]: New customers (by first order date)
  * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
  * [!UICONTROL Perspective]: `Cumulative`
  * [!UICONTROL Metric]: `New customers (by last order date)`
  * [!UICONTROL Filter]:
  * Seconds since customer's last order date >= [Your self-defined cutoff for churned customers]**`^`**
  * `Lifetime number of orders Greater Than 0`

  * [!UICONTROL Metric]: `New customers (by last order date)`
  * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
  * [!UICONTROL Perspective]: Cumulative
  * [!UICONTROL Formula]: `(B / ((A + B) - C)`
  * [!UICONTROL Format]: Percentage

* *Metric `A`: `New customers cumulative`*
* *Metric `B`: `Churned customers by last order date`*
* *Metric `C`: `Customers by last order date cumulative`*
* *`Formula`: `Repeat order probability`*
* *`Time period`: `All time (or custom range)`*
* *`Group by`: `Customer's order number`*
* *`Chart Type`: `Column`*

Below are some common month > second conversions, but google provides other values, including week > seconds conversions for any custom values you may be looking for.

| **Months** | **Seconds** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

After compiling all the reports, you can organize them on the dashboard as you desire. The result may look like the above sample dashboard.
