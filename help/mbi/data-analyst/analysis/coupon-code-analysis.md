---
title: Coupon Performance
description: Learn about analyzing your coupon performance. 
---
# Coupon Performance

Understanding the coupon performance of your business is an interesting way to segment your orders and also better understand your customers. This article will walk you through the steps to create analyses to understand which customers you acquire through the use of coupons, how they perform and track general coupon usage.

![](../../\assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Getting Started

As a first step, you need to ensure that the following columns are synced to your Data Warehouse. If they are not, go ahead and track them, by navigating to "Manage Data" > "Data Warehouse", and syncing the following:

* **sales\_flat\_order** table
* **coupon\_code**
* **base\_discount\_amount**

## Calculated Columns

Columns to create regardless of guest orders policy:

* **sales\_flat\_order** table
* **Order has coupon applied?**
  * Column Type: Same Table => CALCULATION
  * Inputs
    * A: **coupon\_code**

  * Datatype: String
  * Calculation: **case when A is null then 'No coupon' else 'Coupon' end**

* **\[INPUT\] customer\_id - coupon code**
  * Column type: Same Table => CALCULATION
  * Inputs
    * A: **customer\_id**
    * B: **coupon\_code**

  * Datatype: String
  * Calculation: **concat(A,' - ',B)**

* **Number of orders with this coupon**
  * Column Type: Same Table => EVENT\_NUMBER
  * Event Owner:**\[INPUT\] customer\_id - coupon code**
  * Event Rank: **created\_at**
  * Filters: "Orders we count" filter set

Additional columns to create if guest orders NOT supported:

* **customer\_entity** table
  *  **Customer's first order included a coupon? (Coupon/No coupon)**
    * Column Type: Many to One => MAX
    * Path: sales\_flat\_order.customer\_id = customer\_entity.entity\_id
    * Select Column: **Order has coupon applied? (Coupon/No coupon)**
    * Filters:
    * A: Orders we count
    * B: Customer's order number = 1

  * **Customer's first order's coupon**
    * Column Type: Many to One => MAX
    * Path: sales\_flat\_order.customer\_id = customer\_entity.entity\_id
    * Select Column: **coupon\_code**
    * Filter:
    * A: Orders we count
    * B: Customer's order number = 1

  * **Customer's lifetime number of coupons used**
    * Column Type: Many to One => COUNT
    * Path: sales\_flat\_order.customer\_id = customer\_entity.entity\_id
    * Filter:
      * A: Orders we count
      * B: Order has coupon applied? (Coupon/No coupon) = Coupon

  * **Coupon acquisition customer or Non coupon acquisition customer**
    * Column type: Same Table => CALCULATION
    * Inputs
      * A: **Customer's first order included a coupon? (Coupon/No coupon)**

    * Datatype: String
    * Calculation: **case when A='Coupon' then 'Coupon acquisition customer' else 'Non coupon acquisition customer' end**

  * **Percent of customer's orders with coupon**
    * Column type: Same Table => CALCULATION
    * Inputs
      * A: **User's lifetime number of coupons used**
      * B: **User's lifetime number of orders**

    * Datatype: Decimal
    * Calculation: **case when A is null or B is null or B=0 then null else A/B end**

  * **Customer's coupon usage**
    * Column type: Same Table => Calculation
    * Inputs
      * A: **Percent of customer's orders with coupon**

    * Datatype: String
    * Calculation: **case when A is null then null when A=0 then 'Never used coupon' when A<0.5 then 'Mostly full price' when A=0.5 then '50/50' when A=1 then 'Coupons only' when A>0.5 then 'Mostly coupon' else 'Undefined' end**

* **sales\_flat\_order** table
  * **Customer's first order included coupon? (Coupon/No coupon)**
    * Column Type: One to Many => JOINED\_COLUMN
    * Path: sales\_flat\_order.customer\_id = customer\_entity.entity\_id
    * Select Column: **Customer's first order included a coupon? (Coupon/No coupon)**
  ^

  * **Customer's first order's coupon**
    * Column Type: One to Many => JOINED\_COLUMN
    * Path: sales\_flat\_order.customer\_id = customer\_entity.entity\_id
    * Select Column: **Customer's first order coupon?**

Additional columns to create if guest orders NOT supported:

* **sales\_flat\_order** table
  * **Customer's first order included a coupon? (Coupon/No coupon)** **-** created by analyst as part of your \[COUPON ANALYSIS\] ticket
  * **Customer's first order's coupon **{::}**-** created by analyst as part of your \[COUPON ANALYSIS\] ticket

* **Customer's lifetime number of coupons used **{::}**-** created by analyst as part of your \[COUPON ANALYSIS\] ticket
* **Coupon acquisition customer or Non coupon acquisition customer**
  * Column type: Same Table => CALCULATION
  * Inputs
    * A: **Customer's first order included a coupon? (Coupon/No coupon)**

  * Datatype: String
  * Calculation: **case when A='Coupon' then 'Coupon acquisition customer' else 'Non coupon acquisition customer' end**

* **Percent of customer's orders with coupon**
  * Column type: Same Table => CALCULATION
  * Inputs
    * A: **User's lifetime number of coupons used**
    * B: **User's lifetime number of orders**

  * Datatype: Decimal
  * Calculation: **case when A is null or B is null or B=0 then null else A/B end**

* **Customer's coupon usage**
  * Column type: Same Table => Calculation
  * Inputs
    * A: **Percent of customer's orders with coupon**

  * Datatype: String
  * Calculation: **case when A is null then null when A=0 then 'Never used coupon' when A<0.5 then 'Mostly full price' when A=0.5 then '50/50' when A=1 then 'Coupons only' when A>0.5 then 'Mostly coupon' else 'Undefined' end**

## Metrics

* **Coupon discount amount**
  * Orders we count
  * Order has coupon applied? (Coupon/No coupon)= Coupon

* In the **sales\_flat\_order** table
* This metric performs a **Sum**
* On the **discount\_amount** column
* Ordered by the **created\_at** timestamp
* Filter:

* **Number of coupons used**
  * Orders we count
  * Order has coupon applied? (Coupon/No coupon)= Coupon

* In the **sales\_flat\_order** table
* This metric performs a **Count**
* On the **entity\_id** column
* Ordered by the **created\_at** timestamp
* Filter:

Note: Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **% of coupon-acquired and non-coupon-acquired customers**
  * Metric: New customers

* Metric A: Coupon acquisitions
* Time period: All time
* Interval: None
* Group by: Coupon acquisitions customer or Non coupon acquisition customer
* Chart Type: Pie

* **Number of coupon-acquired and non-coupon-acquired customers**
  * Metric: New customers

* Metric A: Coupon acquisitions
* Time period: All time
* Interval: By Month
* Group by: Coupon acquisitions customer or Non coupon acquisition customer
* Chart Type: Stacked column

* **Average lifetime revenue: Coupon Acq. (90+ days age)**
  * Metric: Average lifetime revenue
  * Filter:
  * Customer's first order included a coupon (Coupon/No Coupon) = Coupon

* Metric A: Average lifetime revenue (at least 3 months age)
* Time period: X years ago to 90 days ago
* Interval: None
* Chart Type: Scalar

* **Average lifetime revenue: Non-coupon Acq. (90+ days age)**
  * Metric: Average lifetime revenue
  * Filter:
  * Customer's first order included a coupon (Coupon/No Coupon) = No coupon

* Metric A: Average lifetime revenue (at least 3 months age)
* Time period: X years ago to 90 days ago
* Interval: None
* Chart Type: Scalar

* **Average lifetime revenue by first order coupon**
  * Metric: Average lifetime revenue

* Metric A: Average lifetime revenue
* Time period: All time
* Interval: None
* Group by: Customer's first order's coupon
* Chart Type: Column
* NOTE: If you have a large number of coupon codes, as many of our clients do, you will want to apply a Top/Bottom such as Top 10 sorted by Avg lifetime revenue

* **Repeat order probablility: Coupon acquisitions**
  * Metric: Number of orders
  * Filter:
  * Customer's first order included a coupon (Coupon/No Coupon) = Coupon
  ^

  * Metric: Number of orders
  * Filter:
  * Customer's first order included a coupon (Coupon/No Coupon) = Coupon
  * Is customer's last order? = No
  ^

  * Formula: B/A
  * Format: Percentage %
  ^

  * Select statistically significant number from "Customer's by lifetime orders" chart. When looking at the chart, as a good rule we typically look for order numbers with 30 or more customers in the bucket. Depending on your data set, this may be a large number so feel free to add 1-10.

* Metric A: Number of orders
* Metric B: Number of non last orders
* Formula: Repeat order probability
* Time period: All time
* Interval: None
* Group by: Customer's order number
* Chart Type: Bar chart

* **Repeat order probability: Non-coupon acquisitions**
  * Metric: Number of orders
  * Filter:
  * Customer's first order included a coupon (Coupon/No Coupon) = No Coupon
  ^

  * Metric: Number of orders
  * Filter:
  * Customer's first order included a coupon (Coupon/No Coupon) = No Coupon
  * Is customer's last order? = No
  ^

  * Formula: B/A
  * Format: Percentage %
  ^

  * Select statistically significant number from "Customer's by lifetime orders" chart or 1-5

* Metric A: Number of orders
* Metric B: Number of non last orders
* Formula: Repeat order probability
* Time period: All time
* Interval: None
* Group by: Customer's order number
* Chart Type: Bar chart

* **Coupon-acquired customers' coupon usage rate (repeat orders)**
  * Metric: New customers
  * Filter:
  * Coupon acquisition customer or Non coupon acquisition customer = Coupon acquisition
  ^

  * Metric: Number of orders
  * Filter:
  * Customer's order number > 1
  * Customer's first order included a coupon? (Coupon/No coupon) = Coupon
  ^

  * Metric: Number of orders
  * Filter:
  * Customer's order number > 1
  * Customer's first order included a coupon? (Coupon/No coupon) = Coupon
  * Order has coupon applied? (Coupon/No coupon) = Coupon
  ^

  * Formula: C/B
  * Format: Percentage %

* Metric A: Coupon-acquired customers
* Metric B: Number of repeat orders
* Metric C: Number of repeat orders with coupon
* Formula: % of repeat orders with coupon
* Time period: All time
* Interval: None
* Chart Type: Table (can transpose this table for better visualization)

* **Non-coupon-acquired customers' coupon usage rate (repeat orders)**
  * Metric: New customers
  * Filter:
  * Coupon acquisition customer or Non coupon acquisition customer = Non coupon acquisition
  ^

  * Metric: Number of orders
  * Filter:
  * Customer's order number > 1
  * Customer's first order included a coupon? (Coupon/No coupon) = No coupon
  ^

  * Metric: Number of orders
  * Filter:
  * Customer's order number > 1
  * Customer's first order included a coupon? (Coupon/No coupon) = No Coupon
  * Order has coupon applied? (Coupon/No coupon) = Coupon
  ^

  * Formula: C/B
  * Format: Percentage %

* Metric A: Non-coupon-acquired customers
* Metric B: Number of repeat orders
* Metric C: Number of repeat orders with coupon
* Formula: % of repeat orders with coupon
* Time period: All time
* Interval: None
* Chart Type: Table (can transpose this table for better visualization)

* **Coupon usage details (first time orders)**
  * Metric: Number of orders
  * Filter:
  * Customer's order number = 1
  * Number of orders with this coupon > 10
  ^

  * Metric: Revenue
  * Filter:
  * Customer's order number = 1
  * Number of orders with this coupon > 10
  ^

  * Metric: Coupon discount amount
  * Filter:
  * Customer's order number = 1
  * Number of orders with this coupon > 10
  ^

  * Formula: B-C (if C is negative); B+C (if C is positive)
  * Format: Currency
  ^

  * Metric: Average order value
  * Filter:
  * Customer's order number = 1
  * Number of orders with this coupon > 10

* Metric A: First time orders (FTO)
* Metric B: Revenue from FTO
* Metric C: Discounts applied to FTO
* Formula: Gross revenue from FTO
* Metric E: Average order value for FTO
* Time period: All time
* Interval: None
* Group by: coupon code
* Chart Type: Table
* **Note**: The quantity of 10 for "Number of orders with this coupon" is arbitrary. Feel free to use the most appropriate quantity for this filter.

* **Number of orders with coupon (all time)**
  * Metric: Number of coupons used

* Metric A: Number or orders with coupon
* Time period: All time
* Interval: None
* Chart Type: Scalar

* **Net revenue from orders with coupons (all time)**
  * Metric: Revenue
  * Filter:
  * Order has coupon applied? (Coupon/No coupon) = Coupon

* Metric A: Net revenue from orders with coupons
* Time period: All time
* Interval: None
* Chart Type: Scalar

* **Discounts from coupons (all time)**
  * Metric: Number of coupons used

* Metric A: Coupon discount amount
* Time period: All time
* Interval: None
* Chart Type: Scalar

* **Number of orders with and without coupons**
  * Metric: Number of orders

* Metric A: Number of orders
* Time period: Last 24 months
* Interval: None
* Group by: Order has coupon applied? (Coupon/No coupon)
* Chart Type: Stacked column

* **Coupon usage among repeat users**
  * Metric: New customers
  * Filter:
  * Customer's lifetime number of orders > 1

* Metric A: New customers
* Time period: All time
* Interval: None
* Group by: Customer's coupon usage
* Chart Type: Pie

* **Coupon usage details**
  * Metric: Number of orders with coupon
  * Filter:
  * Number of orders with this coupon > 10
  ^

  * Metric: Revenue
  * Filter:
  * Number of orders with this coupon > 10
  ^

  * Metric: Coupon discount amount
  * Filter:
  * Number of orders with this coupon > 10
  ^

  * Formula: B-C (if C is negative); B+C (if C is positive)
  * Format: Currency
  ^

  * Formula: C/(B-C) (if C is negative); C/(B+C) (if C is positive)
  * Format: Percentage
  ^

  * Metric: Average order value
  * Filter:
  * Number of orders with this coupon > 10
  ^

  * Formula: C/A
  * Format: Currency
  ^

  * Metric: Distinct buyers
  * Filter:
  * Number of orders with this coupon > 10

* Metric A: Number of orders
* Metric B: Net revenue from orders
* Metric C: Total discounts applied
* Formula: Gross revenue
* Formula: % discounted
* Metric F: Average net order value
* Formula: Average order discount
* Metric H: Distinct buyers
* Time period: All time
* Interval: None
* Group by: coupon code
* Chart Type: Table
* Note: The quantity of 10 for "Number of orders with this coupon" is arbitrary. Feel free to use the most appropriate quantity for this filter.

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the image at the top of the page.

If you run into any questions while building this analysis, or simply want to engage our professional services team, [contact support](../../getting-started/support.md).
