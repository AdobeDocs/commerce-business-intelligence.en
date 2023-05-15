---
title: Free shipping threshold
description: Learn how to set up a dashboard that track the performance of your free shipping threshold.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
---
# Free Shipping

>[!NOTE]
>
>This article contains instructions for clients that are using the original architecture and new architecture. You are on the new architecture if you have the "Data Warehouse Views" section available after selecting "Manage Data" from the main toolbar.

This article demonstrates how to set up a dashboard that track the performance of your free shipping threshold. This dashboard, shown below, is a great way to A/B test two free shipping thresholds. For example, your company might be unsure whether you should offer free shipping at $50 or $100. You should perform an A/B test of two random subsets of your customers, and perform the analysis in [!DNL Commerce Intelligence].

Before getting started, you want to identify two separate time periods where you have had different values for your store's free shipping threshold.

![](../../assets/free_shipping_threshold.png)

This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Calculated Columns

If you are on the original architecture (for example, if you do not have the `Data Warehouse Views` option under the `Manage Data` menu), you want to reach out to the support team to build out the below columns. On the new architecture, these columns can be created from the `Manage Data > Data Warehouse` page. Detailed instructions are given below.

* **`sales_flat_order`** table
  * This calculation creates buckets in increments relative to your typical cart sizes. This can range from increments including, 5, 10, 50, 100

* **`Order subtotal (buckets)`** Original Architecture: created by an analyst as part of your `[FREE SHIPPING ANALYSIS]` ticket
* **`Order subtotal (buckets)`** New Architecture:
  * As mentioned above, this calculation creates buckets in increments relative to your typical cart sizes. If you have a native subtotal column such as `base_subtotal`, that can be used as the basis of this new column. If not, it can be a calculated column that excludes shipping and discounts from revenue. 

   >[!NOTE]
   >
   >The "bucket" sizes depend on what is appropriate for you as a client. You could start with your `average order value` and create some buckets less than and greater than that amount. When looking at the calculation below, you see how to easily copy part of the query, edit it, and create additional buckets. The example is done in increments of 50.

  * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`, or `calculated column`, `Datatype`: `Integer`
  * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
    when `A< 200` and `A <= 250` then `201 - 250`
    when `A<251` and `A<= 300` then `251 - 300`
    when `A<301` and `A<= 350` then `301 - 350`
    when `A<351` and `A<=400` then `351 - 400`
    when `A<401` and `A<=450` then `401 - 450`
    else 'over 450'
    end


## Metrics

No new metrics!!!

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **Average order value with shipping rule A**
  * [!UICONTROL Metric]: `Average order value`

* Metric `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Scalar`

* **Number of orders by subtotal buckets with shipping rule A**
  * [!UICONTROL Metric]: `Number of orders`

  >[!NOTE]
  >
  >You can cut off the tail end by showing the top `X` `sorted by` `Order subtotal` (buckets) in the `Show top/bottom`.

* Metric `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* [!UICONTROL Chart Type]: `Column`

* **Percent of orders by subtotal with shipping rule A**
  * [!UICONTROL Metric]: `Number of orders`

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Group by]: `Independent`
  * [!UICONTROL Formula]: `(A / B)`
  * [!UICONTROL Format]: `%`

* Metric `A`: `Number of orders by subtotal (hide)`
* Metric `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* [!UICONTROL Chart Type]: `Line`

* **Percent of orders with subtotal exceeding shipping rule A**
  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Perspective]: `Cumulative`

  * [!UICONTROL Metric]: `Number of orders`
  * [!UICONTROL Group by]: `Independent`

  * [!UICONTROL Formula]: `1- (A / B)`
  * [!UICONTROL Format]: `%`

* Metric `A`: `Number of orders by subtotal`
* Metric `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* [!UICONTROL Chart Type]: `Line`


Repeat the above steps and reports for Shipping B and the time period with shipping rule B.

After compiling all the reports, you can organize them on the dashboard as you desire. The result may look like the image at the top of this page.
