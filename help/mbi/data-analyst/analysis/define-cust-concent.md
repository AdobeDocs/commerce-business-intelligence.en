---
title: Define customer concentration
description: Learn how to set up a dashboard that helps you measure how total revenue is distributed among your customer base.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/kayq-ci-AiHHgNoaX09h6dqKQX14MudLvEqFmos3hQE
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
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
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
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Customer Concentration

This topic demonstrates how to set up a dashboard that helps you measure how total revenue is distributed among your customer base. Understand what percent of customers contribute what percent of revenue and create segmented lists to best market to and retain your high contributing customers.

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Getting Started

You need to first upload a file containing just a primary key with the value of one. This allows the creation of some necessary calculated columns for the analysis.

You can use [the file uploader](../importing-data/connecting-data/using-file-uploader.md) and the image below to format your file.

## Calculated Columns

If you are on the original architecture (for example, if you do not have the `Data Warehouse Views` option under the `Manage Data` menu), you want to contact the support team to build out the below columns. On the new architecture, these columns can be created from the `Manage Data > Data Warehouse` page. Detailed instructions are given below.

A further distinction is made if your business allows guest orders. If so, you can ignore all steps for the `customer_entity` table. If guest orders are not allowed, ignore all steps for the `sales_flat_order` table.

Columns to create

* `Sales_flat_order/customer_entity` table
* (input) `reference`
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `entity_id`
* [!UICONTROL Calculation]: - **case when A is null then null else 1 end**
* [!UICONTROL Datatype]: – `Integer`

* `Customer concentration` table (this is the file you uploaded with the number `1`)
* Number of customers
* [!UICONTROL Column type]: – `Many to One > Count Distinct`
* Path – `sales_flat_order.(input) reference > Customer Concentration.Primary Key` OR `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Selected column – `sales_flat_order.customer_email` OR `customer_entity.entity_id`

* `customer_entity` table
* Number of customers
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Path – `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Selected column – `Number of customers`

* (input) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: – `Same table > Event Number`
* Event owner – `Number of customers`
* Event rank – `Customer's lifetime revenue`

* Customer's revenue percentile
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: – **case when A is null then null else (A/B)*100 end**
* [!UICONTROL Datatype]: – `Decimal`

* `Sales_flat_order` table
* Number of customers
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Path – `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Selected column – `Number of customers`

* (input) Ranking by customer lifetime revenue
* [!UICONTROL Column type]: – `Same table > Event Number`
* Event owner – `Number of customers`
* Event Rank – `Customer's lifetime revenue`
* Filter – `Customer's order number = 1`

* Customer's revenue percentile
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: – **case when A is null then null else (A/B)*100 end**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>The percentiles used are even splits of customers, representing the Xth percentile of your customer base. Each customer is associated with an integer from 1 to 100, which can be thought of as their lifetime revenue *rank*. For example, if the Customer's revenue percentile for a specific customer is **5**, this customer is in the ***fifth percentile*** of all customers in terms of lifetime revenue.

## Metrics

* **Total customer lifetime value**
* In the `customer_entity` table
* This metric performs a **Sum**
* On the `Customer's lifetime revenue` column
* Ordered by the `Customer's first order date` timestamp

## Reports

* **Customer concentration**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Group by]: `Independent`
* Metric `A`: `Total customer lifetime revenue by percentile`
* Metric `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* Show top/bottom: `100% of Customer's revenue percentile Name`
* [!UICONTROL Chart type]: `Line`

* **Top 10% concentration**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* Metric `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* Hide chart
* [!UICONTROL Group by]: `Email`
* [!UICONTROL Chart type]: `Table`

* **Bottom 50% concentration with only one purchase**

* Metric `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* Hide chart
* [!UICONTROL Group by]: `Email`
* [!UICONTROL Chart type]: `Table`

* **Bottom 10% concentration**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* Metric `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* Hide chart
* [!UICONTROL Group by]: `Email`
* [!UICONTROL Chart type]: `Table`

After compiling all the reports, you can organize them on the dashboard as you desire. The result may look like the above sample dashboard.

If you run into any questions while building this analysis, or simply want to engage the Professional Services team, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
