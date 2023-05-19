---
title: Coupon Code Analysis (basic)
description: Learn about the coupon performance of your business is an interesting way to segment your orders and better understand customer habits.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
---
# Basic Coupon Code Analysis

Understanding the coupon performance of your business is an interesting way to segment your orders and better understand customer habits.

This topic documents the steps required to create this analysis to understand how coupon-acquired customers perform, see trends, and track individual coupon code usage.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Getting Started

First, a note about how coupon codes are tracked. If a customer applied a coupon to an order, three things happen:

* A discount is reflected in the `base_grand_total` amount (your `Revenue` metric in Commerce Intelligence)
* The coupon code is stored in the `coupon_code` field. If this field is NULL (empty), the order does not have a coupon associated with it.
* The discounted amount is stored in `base_discount_amount`. Depending on your configuration, this value may appear negative or positive.

## Building a Metric

The first step is to construct a new metric with the following steps:

* Navigate to **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Select the `sales_order`.
* This metric performs a **Sum** on the **base_discount_amount** column, ordered by **created_at**.
  * [!UICONTROL Filters]:
    * Add the `Orders we count` (Saved Filter Set)
    * Add the following:
      * `coupon_code`**IS NOT**`[NULL]`
    * Give the metric a name, such as `Coupon discount amount`.

## Creating your Dashboard

* Once the metric has been created:
  * Navigate to [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
  * Give the dashboard a name such as `_Coupon Analysis_`.

* This is where you create and add all the reports.

## Building Reports

* **New Reports:**

>[!NOTE]
>
>The [!UICONTROL Time Period]** for each report is listed as `All-time`. Feel free to alter this to suit your analysis needs. Adobe recommends all reports on this dashboard cover the same time period, such as `All time`, `Year-to-date`, or `Last 365 days`.

* **Orders with coupons**
  * [!UICONTROL Metric]:`Orders`
    * Add filter:
      * [`A`] `coupon_code` **IS NOT** `[NULL]`

  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]: `None`
  * [!UICONTROL Chart type]:`Number (scalar)`

* **Orders without coupons**
  * [!UICONTROL Metric]: `Orders`
    * Add filter:
      * [`A`] `coupon_code` **IS** `[NULL]`

  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]:`None`
  * [!UICONTROL Chart type]:`Number (scalar)`

* **Net revenue from orders with coupons**
  * [!UICONTROL Metric]: `Revenue`
    * Add filter:
      * [`A`] `coupon_code` **IS NOT** `[NULL]`

  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]: `None`
  * [!UICONTROL Chart type]: `Number (scalar)`

* **Discounts from coupons**
  * [!UICONTROL Metric]: `Coupon discount amount`
  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]: `None`
  * [!UICONTROL Chart type]: `Number (scalar)`

* **Average lifetime revenue: Coupon acquired customers**
  * [!UICONTROL Metric]: `Avg lifetime revenue`
    * Add filter:
      * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`

  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]: `None`
  * [!UICONTROL Chart type]: `Number (scalar)`

* **Average lifetime revenue: Non-coupon acquired customers**
  * [!UICONTROL Metric]: `Avg lifetime revenue`
    * Add filter:
      * [A] `Customer's first order's coupon_code` **IS**`[NULL]`

  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]: `None`
  * [!UICONTROL Chart type]: `Number (scalar)`

* **Coupon usage details (first time orders)**
  * Metric `1`: `Orders`
    * Add filter:
      * [`A`] `coupon_code` **IS NOT**`[NULL]`
      * [`B`] `Customer's order number` **Equal to** `1`

  * Metric `2`: `Revenue`
    * Add filter:
      * [`A`] `coupon_code` **IS NOT**`[NULL]`
      * [`B`] `Customer's order number` **Equal to** `1`

    * Rename:  `Net revenue`

  * Metric `3`: `Coupon discount amount`
    * Add filter:
      * [`A`] `coupon_code` **IS NOT**`[NULL]`
      * [`B`] `Customer's order number` **Equal to** `1`

  * Create formula: `Gross revenue`
    * [!UICONTROL Formula]: `(B – C)`
    * [!UICONTROL Format]: `Currency`

  * Create formula:**% discounted**
    * Formula: `(C / (B - C))`
    * [!UICONTROL Format]: `Percentage`

  * Create formula: `Average order discount`
    * [!UICONTROL Formula]: `(C / A)`
    * [!UICONTROL Format]: `Percentage`

  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]: `None`
  * [!UICONTROL Chart type]: `Table`

* **Average lifetime revenue by first order coupon**
  * [!UICONTROL Metric]:**Avg lifetime revenue**
    * Add filter:
      * [`A`] `coupon_code` **IS**`[NULL]`

  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]: `None`
  * [!UICONTROL Chart type]: `Number (scalar)`

* **Coupon usage details (first time orders)**
  * [!UICONTROL Metric]: `Avg lifetime revenue`
    * Add filter:
      * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`

  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]: `None`
  * [!UICONTROL Group by]: `Customer's first order's coupon_code`
  * [!UICONTROL Chart type]:**Column**

* **New customers by coupon / non-coupon acquisition**
  * Metric `1`: `New customers`
    * Add filter:
      * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`

    * [!UICONTROL Rename]: `Coupon acquisition customer`

  * Metric `2`: `New customers`
    * Add filter:
      * [`A`] `coupon_code` **IS**`[NULL]`

    * [!UICONTROL Rename]: `Non-coupon acquisition customer`

  * [!UICONTROL Time period]: `All time`
  * [!UICONTROL Interval]: `By Month`
  * [!UICONTROL Chart type]: `Stacked Column`

After building the reports, refer to the image at the top of this topic for how you can organize the reports on your dashboard.
