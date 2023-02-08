---
title: Coupon Performance
description: Learn about analyzing your coupon performance.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
---
# Advanced Coupon Code Analysis

Understanding the coupon performance of your business is an interesting way to segment your orders and also better understand your customers. This article will walk you through the steps to create analyses to understand which customers you acquire through the use of coupons, how they perform and track general coupon usage.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Getting Started

As a first step, you need to ensure that the following columns are synced to your Data Warehouse. If they are not, go ahead and track them, by navigating to "Manage Data" > "Data Warehouse", and syncing the following:

* **sales\_flat\_order** table
* **coupon\_code**
* **base\_discount\_amount**

## Calculated Columns

Columns to create regardless of guest orders policy:

* `sales\_flat\_order` table
* **Order has coupon applied?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
  * [!UICONTROL Inputs]:
    * `A`: `coupon\_code`

  * [!UICONTROL Datatype]:: `String`
  * [!UICONTROL Calculation]:: case when `A` is null then `No coupon` else `Coupon` end

* **\[INPUT\] customer\_id - coupon code**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
  * [!UICONTROL Inputs]:
    * `A`: `customer\_id`
    * `B`: `coupon\_code`

  * [!UICONTROL Datatype]:: String
  * [!UICONTROL Calculation]:: `concat(A,' - ',B)`

* **Number of orders with this coupon**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
  * Event Owner:`INPUT customer_id - coupon code`
  * Event Rank: `created\_at`
  * [!UICONTROL Filters]: `Orders we count` filter set

Additional columns to create if guest orders NOT supported:

* `customer\_entity` table
  *  **Customer's first order included a coupon? (Coupon/No coupon)**
    * [!UICONTROL Column type]: `Many to One => MAX`
    * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
    * Select a [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
    * [!UICONTROL Filters]:
       * `A`: `Orders we count`
       * `B`: `Customer's order number = 1`

  * **Customer's first order's coupon**
    * [!UICONTROL Column type]: `Many to One => MAX`
    * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
    * Select a [!UICONTROL column]: `coupon\_code`
    * [!UICONTROL Filter]:
       * `A`: `Orders we count`
       * `B`: `Customer's order number = 1`

  * **Customer's lifetime number of coupons used**
    * [!UICONTROL Column type]: `Many to One => COUNT`
    * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
    * [!UICONTROL Filter]:
      * `A`: `Orders we count`
      * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

  * **Coupon acquisition customer or Non coupon acquisition customer**
    * [!UICONTROL Column type]: `Same Table => CALCULATION`
    * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

    * [!UICONTROL Datatype]:: `String`
    * [!UICONTROL Calculation]:: **case when A='Coupon' then 'Coupon acquisition customer' else 'Non coupon acquisition customer' end**

  * **Percent of customer's orders with coupon**
    * [!UICONTROL Column type]: `Same Table => CALCULATION`
    * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

    * [!UICONTROL Datatype]:: `Decimal`
    * [!UICONTROL Calculation]:: **case when A is null or B is null or B=0 then null else A/B end**

  * **Customer's coupon usage**
    * [!UICONTROL Column type]: `Same Table => Calculation`
    * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

    * [!UICONTROL Datatype]:: `String`
    * [!UICONTROL Calculation]:: **case when A is null then null when A=0 then 'Never used coupon' when A<0.5 then 'Mostly full price' when A=0.5 then '50/50' when A=1 then 'Coupons only' when A>0.5 then 'Mostly coupon' else 'Undefined' end**

* `sales\_flat\_order` table
  * **Customer's first order included coupon? (Coupon/No coupon)**
    * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
    * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
    * Select a [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
  ^

  * **Customer's first order's coupon**
    * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
    * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
    * Select a [!UICONTROL column]: `Customer's first order coupon?`

Additional columns to create if guest orders NOT supported:

* `sales\_flat\_order` table
  * **Customer's first order included a coupon? (Coupon/No coupon)** **-** created by analyst as part of your \[COUPON ANALYSIS\] ticket
  * **Customer's first order's coupon **{::}**-** created by analyst as part of your \[COUPON ANALYSIS\] ticket

* **Customer's lifetime number of coupons used **{::}**-** created by analyst as part of your \[COUPON ANALYSIS\] ticket
* **Coupon acquisition customer or Non coupon acquisition customer**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
  * [!UICONTROL Inputs]:
    * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

  * [!UICONTROL Datatype]:: `String`
  * [!UICONTROL Calculation]:: **case when A='Coupon' then 'Coupon acquisition customer' else 'Non coupon acquisition customer' end**

* **Percent of customer's orders with coupon**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
  * [!UICONTROL Inputs]:
    * `A`: `User's lifetime number of coupons used`
    * `B`: `User's lifetime number of orders`

  * [!UICONTROL Datatype]:: `Decimal`
  * [!UICONTROL Calculation]:: **case when A is null or B is null or B=0 then null else A/B end**

* **Customer's coupon usage**
   * [!UICONTROL Column type]: `Same Table => Calculation`
  * [!UICONTROL Inputs]:
    * `A`: `Percent of customer's orders with coupon`

  * [!UICONTROL Datatype]:: `String`
  * [!UICONTROL Calculation]:: **case when A is null then null when A=0 then 'Never used coupon' when A<0.5 then 'Mostly full price' when A=0.5 then '50/50' when A=1 then 'Coupons only' when A>0.5 then 'Mostly coupon' else 'Undefined' end**

## Metrics

* **Coupon discount amount**
  * `Orders we count`
  * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* In the `sales\_flat\_order` table
* This metric performs a **Sum**
* On the `discount\_amount` column
* Ordered by the `created\_at` timestamp
* [!UICONTROL Filter]:

* **Number of coupons used**
  * `Orders we count`
  * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* In the `sales\_flat\_order` table
* This metric performs a **Count**
* On the `entity\_id` column
* Ordered by the `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **% of coupon-acquired and non-coupon-acquired customers**
  * [!UICONTROL Metric]: `New customers`

* Metric `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` or `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Pie`

* **Number of coupon-acquired and non-coupon-acquired customers**
  * [!UICONTROL Metric]: `New customers`

* Metric A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` or `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Average lifetime revenue: Coupon Acq. (90+ days age)**
  * [!UICONTROL Metric]: `Average lifetime revenue`
  * [!UICONTROL Filter]: 
     * Customer's first order included a coupon (Coupon/No Coupon) = Coupon

* Metric `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart type]: `Scalar`

* **Average lifetime revenue: Non-coupon Acq. (90+ days age)**
  * [!UICONTROL Metric]: Average lifetime revenue
  * [!UICONTROL Filter]:
     * Customer's first order included a coupon (Coupon/No Coupon) = No coupon

* Metric `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart type]: `Scalar`

* **Average lifetime revenue by first order coupon**
  * [!UICONTROL Metric]: `Average lifetime revenue`

* Metric `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* [!UICONTROL Chart type]: `Column`

>[!NOTE]
>
>If you have a large number of coupon codes, as many of our clients do, you will want to apply a Top/Bottom such as Top 10 sorted by Avg lifetime revenue

* **Repeat order probablility: Coupon acquisitions**
  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Filter]:
     * Customer's first order included a coupon (Coupon/No Coupon) = Coupon

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Filter]:
     * Customer's first order included a coupon (Coupon/No Coupon) = Coupon
     * Is customer's last order? = No
  * [!UICONTROL Formula]: `B/A`
  * [!UICONTROL Format]: `Percentage %`

  * Select statistically significant number from `Customer's by lifetime orders` chart. When looking at the chart, as a good rule we typically look for order numbers with 30 or more customers in the bucket. Depending on your data set, this may be a large number so feel free to add 1-10.

* Metric `A`: `Number of orders`
* Metric `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Repeat order probability: Non-coupon acquisitions**
  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Filter]:
     * Customer's first order included a coupon (Coupon/No Coupon) = No Coupon

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Filter]:
     * Customer's first order included a coupon (Coupon/No Coupon) = No Coupon
     * Is customer's last order? = No

  * [!UICONTROL Formula]: `B/A`
  * [!UICONTROL Format]: `Percentage %`

  * Select statistically significant number from `Customer's by lifetime orders` chart or 1-5.

* Metric `A`: `Number of orders`
* Metric `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Coupon-acquired customers' coupon usage rate (repeat orders)**
  * [!UICONTROL Metric]: `New customers`
  * [!UICONTROL Filter]:
     * Coupon acquisition customer or Non coupon acquisition customer = Coupon acquisition

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Filter]:
     * Customer's order number > 1
     * Customer's first order included a coupon? (Coupon/No coupon) = Coupon

  * [!UICONTROL Metric]:`Number of orders`
  * [!UICONTROL Filter]:
     * Customer's order number > 1
     * Customer's first order included a coupon? (Coupon/No coupon) = Coupon
     * Order has coupon applied? (Coupon/No coupon) = Coupon

  * [!UICONTROL Formula]: `C/B`
  * [!UICONTROL Format]: `Percentage %`

* Metric `A`: `Coupon-acquired customers`
* Metric `B`: `Number of repeat orders`
* Metric `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart type]: `Table` (can transpose this table for better visualization)

* **Non-coupon-acquired customers' coupon usage rate (repeat orders)**
  * [!UICONTROL Metric]: `New customers`
  * [!UICONTROL Filter]:
     * Coupon acquisition customer or Non coupon acquisition customer = Non coupon acquisition

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Filter]:
     * Customer's order number > 1
     * Customer's first order included a coupon? (Coupon/No coupon) = No coupon

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Filter]:
     * Customer's order number > 1
     * Customer's first order included a coupon? (Coupon/No coupon) = No Coupon
     * Order has coupon applied? (Coupon/No coupon) = Coupon

  * [!UICONTROL Formula]: `C/B`
  * [!UICONTROL Format]: `Percentage %`

* Metric `A`: `Non-coupon-acquired customers`
* Metric `B`: `Number of repeat orders`
* Metric `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart type]: `Table` (can transpose this table for better visualization)

* **Coupon usage details (first time orders)**
  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Filter]:
     * Customer's order number = 1
     * Number of orders with this coupon > 10

  * [!UICONTROL Metric]: `Revenue`
  * [!UICONTROL Filter]:
     * Customer's order number = 1
     * Number of orders with this coupon > 10

  * [!UICONTROL Metric]: `Coupon discount amount`
  * [!UICONTROL Filter]:
     * Customer's order number = 1
     * Number of orders with this coupon > 10

  * [!UICONTROL Formula]: `B-C` (if C is negative); B+C (if C is positive)
  * [!UICONTROL Format]: `Currency`

  * [!UICONTROL Metric]: `Average order value`
  * [!UICONTROL Filter]:
     * Customer's order number = 1
     * Number of orders with this coupon > 10

* Metric `A`: `First time orders (FTO)`
* Metric `B`: `Revenue from FTO`
* Metric `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* Metric `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `coupon code`
* [!UICONTROL Chart type]: `Table`
>[!NOTE]
>
>The quantity of 10 for "Number of orders with this coupon" is arbitrary. Feel free to use the most appropriate quantity for this filter.

* **Number of orders with coupon (all time)**
  * [!UICONTROL Metric]: `Number of coupons used`

* Metric `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart type]: `Scalar`

* **Net revenue from orders with coupons (all time)**
  * [!UICONTROL Metric]: `Revenue`
  * [!UICONTROL Filter]:
     * Order has coupon applied? (Coupon/No coupon) = Coupon

* Metric `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart type]: `Scalar`

* **Discounts from coupons (all time)**
  * [!UICONTROL Metric]: `Number of coupons used`

* Metric `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart type]: `Scalar`

* **Number of orders with and without coupons**
  * [!UICONTROL Metric]: `Number of orders`

* Metric `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Coupon usage among repeat users**
  * [!UICONTROL Metric]: `New customers`
  * [!UICONTROL Filter]:
     * Customer's lifetime number of orders > 1

* Metric `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* [!UICONTROL Chart type]: `Pie`

* **Coupon usage details**
  * [!UICONTROL Metric]: `Number of orders with coupon`
  * [!UICONTROL Filter]:
     * Number of orders with this coupon > 10

  * [!UICONTROL Metric]: `Revenue`
  * [!UICONTROL Filter]:
     * Number of orders with this coupon > 10

  * [!UICONTROL Metric]: `Coupon discount amount`
  * [!UICONTROL Filter]:
     * Number of orders with this coupon > 10

  * [!UICONTROL Formula]: `B-C` (if `C` is negative); `B+C` (if `C` is positive)
  * [!UICONTROL Format]: `Currency`

  * [!UICONTROL Formula]: `C/(B-C)` (if `C` is negative); `C/(B+C)` (if `C` is positive)
  * [!UICONTROL Format]: `Percentage`

  * [!UICONTROL Metric]: `Average order value`
  * [!UICONTROL Filter]:
     * Number of orders with this coupon > 10

  * [!UICONTROL Formula]: `C/A`
  * [!UICONTROL Format]: `Currency`

  * [!UICONTROL Metric]: `Distinct buyers`
  * [!UICONTROL Filter]:
     * Number of orders with this coupon > 10

* Metric `A`: `Number of orders`
* Metric `B`: `Net revenue from orders`
* Metric `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* Metric `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* Metric `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `coupon code`
* [!UICONTROL Chart type]: `Table`

>[!NOTE]
>
>The quantity of 10 for "Number of orders with this coupon" is arbitrary. Feel free to use the most appropriate quantity for this filter.

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the image at the top of the page.

If you run into any questions while building this analysis, or simply want to engage our professional services team, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
