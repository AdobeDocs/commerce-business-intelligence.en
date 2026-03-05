---
title: Recency, Frequency, Monetary (RFM) Analysis
description: Learn how to set up a dashboard that allows you to segment your customers by their recency, frequency, and monetary rankings.
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/AaRzdTdV7-a4ApO-TA5jbyaJ3sr6sqP9HCToKG--uQ0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
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
---
# RFM Analysis

This topic demonstrates how to set up a dashboard that allows you to segment your customers by their recency, frequency, and monetary rankings. RFM analysis is a marketing technique that takes customer behaviors into account to help you determine segmentation for outreach. It accounts for three aspects:

1. Recency in how recently a customer purchased from your store
1. Frequency in how often they purchase from you
1. Monetary in how much the customer spends

![RFM analysis dashboard showing recency, frequency, and monetary value segments](../../assets/blobid0.png)

The RFM analysis can only be configured if you have the [!DNL Adobe Commerce Intelligence] Pro plan on the new architecture (for example, if you have the `Data Warehouse Views` option under the `Manage Data` menu). These columns can be created from the **[!DNL Manage Data > Data Warehouse]** page. Detailed instructions are provided below.

## Getting Started

You need to first upload a file containing just a primary key with the value of one. This allows the creation of some necessary calculated columns for the analysis.

You can use this [article](../importing-data/connecting-data/using-file-uploader.md) and the image below to format your file.

## Calculated Columns

A further distinction is made if your business allows guest orders. If so, you can ignore all steps for the `customer_entity` table. If guest orders are not allowed, ignore all steps for the `sales_flat_order` table.

Columns to create

* **`Sales_flat_order/customer_entity`** table
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* Selected [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

*     Seconds since customer's last order date
* [!UICONTROL Column type]: –     "Same table > Age
* Selected [!UICONTROL column]: `Customer's last order date`

* (input) Count reference
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* [!UICONTROL Datatype]: `Integer`

* **Count reference** table (this is the file you uploaded with the number "1")
* Number of customers
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` OR `customer_entity.(input)reference > Count Reference`. `Primary Key`
* Selected [!UICONTROL column]: `sales_flat_order.customer_email` OR `customer_entity.entity_id`

* **Customer_entity** table
* Number of customers
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.(input) reference > Customer Concentration. `Primary Key`
* Selected [!UICONTROL column]: `Number of customers`

* (input) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* Ranking by customer lifetime revenue
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* [!UICONTROL Datatype]: `Integer`

* Customer's monetary score (by percentiles)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* [!UICONTROL Datatype]: `Integer`

* (input) Ranking by customer lifetime number of orders
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* Ranking by customer lifetime number of orders
* [!UICONTROL Column type]: – "Same table > Calculation"
* [!UICONTROL Inputs]: – **(input) Ranking by customer lifetime number of orders**, **Number of customers**
* [!UICONTROL Calculation]: – **case when A is null then null else (B-(A-1)) end**
* [!UICONTROL Datatype]: – Integer

* Customer's frequency score (by percentiles)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* [!UICONTROL Datatype]: `Integer`

* Ranking by seconds since customer's last order date
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* Customer's recency score (by percentiles)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* [!UICONTROL Datatype]: `Integer`

* Customer's recency score (by percentiles)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* [!UICONTROL Datatype]: String

* **Count reference** table
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` OR `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Selected [!UICONTROL column]: `sales_flat_order.customer_email` OR `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Not Equal To 000

* **Customer_entity** table
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* Selected [!UICONTROL column]: – `Number of customers`

* Customer's recency score `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: – `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* [!UICONTROL Datatype]: `Integer`

* (input) Ranking by customer's overall RFM score
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Not Equal To 000

* Ranking by customer's overall RFM score
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* [!UICONTROL Datatype]: `Integer`

* Customer's RFM group
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* [!UICONTROL Datatype]: `Integer`

>[!NOTE]
>
>The percentiles used are even splits of customers (for example, 20 percent buckets to return 1-5). If you have a custom way you would like to weight these, let the analyst know when you submit the ticket.

## Metrics

No new metrics!

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **Customers by RFM grouping**
* Metric `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* Hide chart
* [!UICONTROL Group by]: `Customer's RFM group`
* [!UICONTROL Group by]: `Email`
* [!UICONTROL Chart type]: `Table`

* **Customers with five recency score**
* Metric `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Scalar`
* Hide chart
* [!UICONTROL Group by]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* [!UICONTROL Chart type]: `Table`

* **Customers with one recency score**
* Metric `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Scalar`
* Hide chart
* [!UICONTROL Group by]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* [!UICONTROL Chart type]: `Table`

After compiling all the reports, you can organize them on the dashboard as you desire. The result may look like the above sample dashboard, but the three generated tables are just examples of the types of customer segmentation you can perform.
