---
title: Recency, Frequency, Monetary (RFM) Analysis
description: Learn how to set up a dashboard that will allow you to segment your customers by their recency, frequency, and monetary rankings. 
---
# RFM Analysis

In this article, we demonstrate how to set up a dashboard that will allow you to segment your customers by their recency, frequency, and monetary rankings. RFM analysis is a marketing technique that takes customer behaviors into account to help you determine segmentation for outreach. It takes three aspects into account: Recency in how recently a customer purchased from your store, Frequency in how often they purchase from you, and Monetary in how much the customer spends.

![](../../assets/blobid0.png)

The RFM analysis is only able to be configured if you have the [!DNL MBI] Pro plan on the new architecture (for example,if you have the "Data Warehouse Views" option under the "Manage Data" menu). These columns can be created from the "Manage Data > Data Warehouse" page. Detailed instructions are given below.

## Getting Started

You will need to first upload a file containing just a primary key with the value of one. This will allow the creation of some necessary calculated columns for the analysis.

You can leverage this [help center article](../importing-data/connecting-data/using-file-uploader.md) as well as the image below to format your file.

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

* **Count reference** table (this is the file you just uploaded with the number "1")
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
>The percentiles used are even splits of customers (for example,20% buckets to return 1-5). If you have a custom way you would like to weight these, let the analyst know when you submit the ticket.

## Metrics

No new metrics!

**Note**: Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

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

* **Customers with 5 recency score**
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

* **Customers with 1 recency score**
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

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the above sample dashboard, but the three generated tables are just examples of the types of customer segmentation you can perform.
