---
title: Recency, Frequency, Monetary (RFM) Analysis
description: Learn how to set up a dashboard that will allow you to segment your customers by their recency, frequency, and monetary rankings. 
---
# RFM Analysis

In this article, we demonstrate how to set up a dashboard that will allow you to segment your customers by their recency, frequency, and monetary rankings. RFM analysis is a marketing technique that takes customer behaviors into account to help you determine segmentation for outreach. It takes three aspects into account: Recency in how recently a customer purchased from your store, Frequency in how often they purchase from you, and Monetary in how much the customer spends.

![](../../assets/blobid0.png)

The RFM analysis is only able to be configured if you have the MBI Pro plan on the new architecture (i.e., if you have the "Data Warehouse Views" option under the "Manage Data" menu). These columns can be created from the "Manage Data > Data Warehouse" page. Detailed instructions are given below.

## Getting Started

You will need to first upload a file containing just a primary key with the value of one. This will allow the creation of some necessary calculated columns for the analysis.

You can leverage this [help center article](../importing-data/connecting-data/using-file-uploader.md) as well as the image below to format your file.

## Calculated Columns

A further distinction is made if your business allows guest orders. If so, you can ignore all steps for the `customer_entity` table. If guest orders are not allowed, ignore all steps for the `sales_flat_order` table.

Columns to create

* **Sales_flat_order/customer_entity**table
* Customer's last order date
* Column type – "Many to one > Max"
* Path – **sales_flat_order.customer_id > customer_entity.entity_id**
* Selected column: **created_at**
* Filter - Orders we count

* Seconds since customer's last order date
* Column type – "Same table > Age"
* Selected column: **Customer's last order date**

* (input) Count reference
* Column type – "Same table > Calculation"
* Inputs – **entity_id**
* Calculation - `**case when A is null then null else 1 end**`
* Datatype – Integer

* **Count reference** table (this is the file you just uploaded with the number "1")
* Number of customers
* Column type – "Many to One > Count Distinct"
* Path – **sales_flat_order.(input) reference > Count reference.Primary Key** OR **customer_entity**.(input)reference > Count Reference. **Primary Key**
* Selected column – **sales_flat_order.customer_email** OR **customer_entity.entity_id**

* **Customer_entity** table
* Number of customers
* Column type – "One to Many > JOINED_COLUMN"
* Path – **customer_entity**.(input) reference > Customer Concentration. **Primary Key**
* Selected column – **Number of customers**

* (input) Ranking by customer lifetime revenue
* Column type –**"Same table > Event Number"
* Event owner – **(input) reference for count**
* Event rank – **Customer's lifetime revenue**

* Ranking by customer lifetime revenue
* Column type – "Same table > Calculation"
* Inputs – **(input) Ranking by customer lifetime revenue**, **Number of customers**
* Calculation – **case when A is null then null else (B-(A-1)) end**
* Datatype – Integer

* Customer's monetary score (by percentiles)
* Column type – "Same table > Calculation"
* Inputs – **(input) Ranking by customer lifetime revenue**, **Number of customers**
* Calculation – **Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end**
* Datatype – Integer

* (input) Ranking by customer lifetime number of orders
* Column type – **"Same table > Event Number"
* Event owner – **(input) reference for count**
* Event rank – **Customer's lifetime number of orders**

* Ranking by customer lifetime number of orders
* Column type – "Same table > Calculation"
* Inputs – **(input) Ranking by customer lifetime number of orders**, **Number of customers**
* Calculation – **case when A is null then null else (B-(A-1)) end**
* Datatype – Integer

* Customer's frequency score (by percentiles)
* Column type – "Same table > Calculation"
* Inputs – **(input) Ranking by customer lifetime number of orders**, **Number of customers**
* Calculation – **Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end**
* Datatype – Integer

* Ranking by seconds since customer's last order date
* Column type** –**"Same table > Event Number"
* Event owner** – (input) reference for count**
* Event rank** – Seconds since customer's last order date**

* Customer's recency score (by percentiles)
* Column type – "Same table > Calculation"
* Inputs – **(input) Ranking by customer lifetime number of orders**, **Number of customers**
* Calculation – **Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end**
* Datatype – Integer

* Customer's recency score (by percentiles)
* Column type – "Same table > Calculation"
* Inputs – **Customer's recency score (by percentiles)**, **Customer's frequency score (by percentiles)**, **Customer's monetary score (by percentiles)**
* Calculation – **case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end**
* Datatype – String

* **Count reference** table
* Number of customers (RFM > 0)
* Column type – "Many to One > Count Distinct"
* Path – **sales_flat_order.(input) reference > Customer Concentration. Primary Key** OR** customer_entity.(input)reference > Customer Concentration.Primary Key**
* Selected column – **sales_flat_order.customer_email** OR **customer_entity.entity_id**
* Filter - **Customer's RFM score (by percentile)** Not Equal To 000

* **Customer_entity** table
* Number of customers (RFM > 0)
* Column type – "One to Many > JOINED_COLUMN"
* Path** – **customer_entity.(input) reference > Customer Concentration.Primary Key**
* Selected column – **Number of customers**

* Customer's recency score (R+F+M)
* Column type – "Same table > Calculation"
* Inputs – **Customer's recency score (by percentiles)**, **Customer's frequency score (by percentiles)**, **Customer's monetary score (by percentiles)**
* Calculation – **case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end**
* Datatype – Integer

* (input) Ranking by customer's overall RFM score
* Column type – **"Same table > Event Number"**
* Event owner – **(input) reference for count**
* Event rank – **Customer's recency score (R+F+M)**
* Filter - **Customer's RFM score (by percentile)** Not Eqaul To 000

* Ranking by customer's overall RFM score
* Column type – "Same table > Calculation"
* Inputs – **(input) Ranking by customer's overall RFM score**, **Number of customers (RFM > 0)**
* Calculation – **case when A is null then null else (B-(A-1)) end**
* Datatype – Integer

* Customer's RFM group
* Column type – "Same table > Calculation"
* Inputs – **(input) Ranking by customer lifetime revenue**, **Number of customers**
* Calculation – **Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end**
* Datatype – Integer

**Note**: The percentiles used are even splits of customers (i.e., 20% buckets to return 1-5). If you have a custom way you would like to weight these, let the analyst know when you submit the ticket.

## Metrics

No new metrics!

**Note**: Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **Customers by RFM grouping**
* *Metric A: New customers*
* Metric: New customers
* Filter:
* Customer's RFM score (by percentiles) Not Equal to 000

* *Time period: All time*
* *Interval: None*
* *Hide chart*
* *Group by: Customer's RFM group*
* *Group by: Email*
* *Chart type: Table*

* **Customers with 5 recency score**
* *Metric A: New customers*
* Metric: New customers
* Filter:
* Customer's recency score (by percentiles) Equal to 5

* *Time period: All time*
* *Interval: None*
* *Chart Type: Scalar*
* *Hide chart*
* *Group by: Email*
* *Group by: Customer's RFM score (R+F+M)*
* *Chart type: Table*

* **Customers with 1 recency score**
* *Metric A: New customers*
* Metric: New customers
* Filter:
* Customer's recency score (by percentiles) Equal to 1

* *Time period: All time*
* *Interval: None*
* *Chart Type: Scalar*
* *Hide chart*
* *Group by: Email*
* *Group by: Customer's RFM score (R+F+M)*
* *Chart type: Table*

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the above sample dashboard, but the three generated tables are just examples of the types of customer segmentation you can perform.
