---
title: Coupon Code Analysis (basic)
description: Learn about the coupon performance of your business is an interesting way to segment your orders and better understand customer habits. 
---
# Basic Coupon Code Analysis

Understanding the coupon performance of your business is an interesting way to segment your orders and better understand customer habits.

We have documented the steps required to create this analysis to understand how coupon-acquired customers perform, see trends, and track individual coupon code usage.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

#### Getting Started

First, a note about how coupon codes are tracked. If a customer applied a coupon to an order, three things happen:

* A discount is reflected in the `base_grand_total` amount (your **Revenue** metric in MBI)<!--</span>-->
* The coupon code is stored in the `coupon_code` field. If this field is NULL (empty) the order does not have a coupon associated with it.
* The discounted amount is stored in `base_discount_amount`. Depending on your configuration, this value may appear negative or positive.

## Building a Metric

The first step will be to construct a new metric with the following steps:<!--</span>-->
* Navigate to **Manage Data > Metrics > Create New Metric**.
* Select the `sales_order` (if your store is on Magento 2) or `sales_flat_order` (if your store is on Magento 1) table.
* This metric performs a **Sum** on the **base_discount_amount** column, ordered by **created_at**.
  * FILTERS:
    * Add the **Orders we count (Saved Filter Set)**
    * Add the following:
      * `coupon_code`**IS NOT**`[NULL]`
    * Give the metric a name, such as **"Coupon discount amount"**.

## Creating your Dashboard

* Once the metric has been created:
  * Navigate to **Dashboards > Dashboard Options > Create New Dashboard**.
  * Give the dashboard a name such as _Coupon Analysis_.

* This will be where we create and add all the reports.

## Building Reports

* **New Reports:**
  * If you have not already, check out [this video][1] about using the Visual Report Builder to build charts, tables, and scalar values.
  * Note on **Time Period**: The time period for each report is listed as "All-time". Please feel free to alter this to suit your analysis needs. We recommend all reports on this dashboard cover the same time period, such as "All time", "Year-to-date", or "Last 365 days".

* **Orders with coupons**
  * Metric:**Orders</em>
    * Add filter:
      * [A] `coupon_code` **IS NOT** `[NULL]`

  * Time period:**All time</em>
  * Interval:**None</em>
  * Chart Type:**Number (scalar)</em>

* **Orders without coupons**
  * Metric:**Orders</em>
    * Add filter:
      * [A] `coupon_code` **IS** `[NULL]`

  * Time period:**All time</em>
  * Interval:**None</em>
  * Chart Type:**Number (scalar)</em>

* **Net revenue from orders with coupons**
  * Metric:**Revenue</em>
    * Add filter:
      * [A] `coupon_code` **IS NOT** `[NULL]`

  * Time period:**All time</em>
  * Interval:**None</em>
  * Chart Type:**Number (scalar)</em>

* **Discounts from coupons**
  * Metric:**Coupon discount amount</em>
  * Time period:**All time</em>
  * Interval:**None</em>
  * Chart Type:**Number (scalar)</em>

* **Average lifetime revenue: Coupon acquired customers**
  * Metric:**Avg lifetime revenue</em>
    * Add filter:
      * [A] `Customer's first order's coupon_code` **IS NOT** `[NULL]`

  * Time period:**All time</em>
  * Interval:**None</em>
  * Chart Type:**Number (scalar)</em>

* **Average lifetime revenue: Non-coupon acquired customers**
  * Metric:**Avg lifetime revenue</em>
    * Add filter:
      * [A] ` Customer's first order's coupon_code` **IS**`[NULL]`

  * Time period:**All time</em>
  * Interval:**None</em>
  * Chart Type:**Number (scalar)</em>

* **Coupon usage details (first time orders)**
  * Metric 1:**Orders</em>
    * Add filter:
      * [A] `coupon_code` **IS NOT**`[NULL]`
      * [B] `Customer's order number` **Equal to** `1`

  * Metric 2:**Revenue</em>
    * Add filter:
      * [A] `coupon_code` **IS NOT**`[NULL]`
      * [B] `Customer's order number` **Equal to** `1`

    * Rename: *Net revenue*

  * Metric 3:**Coupon discount amount</em>
    * Add filter:
      * [A] `coupon_code` **IS NOT**`[NULL]`
      * [B] `Customer's order number` **Equal to** `1`

  * Create new formula:**Gross revenue</em>
    * Formula:**(B – C)</em>
    * Format:**Currency</em>

  * Create new formula:**% discounted</em>
    * Formula*: (C / (B - C))*
    * Format:**Percentage</em>

  * Create new formula:**Average order discount</em>
    * Formula:**(C / A)</em>
    * Format:**Percentage</em>

  * Time period:**All time</em>
  * Interval:**None</em>
  * Chart Type:**Table</em>

* **Average lifetime revenue by first order coupon**
  * Metric:**Avg lifetime revenue</em>
    * Add filter:
      * [A] `coupon_code` **IS**`[NULL]`

  * Time period:**All time</em>
  * Interval:**None</em>
  * Chart Type:**Number (scalar)</em>

* **Coupon usage details (first time orders)**
  * Metric:**Avg lifetime revenue</em>
    * Add filter:
      * [A] `Customer's first order's coupon_code` **IS NOT** `[NULL]`

  * Time period:**All time</em>
  * Interval:**None</em>
  * Group by:**Customer's first order's coupon_code</em>
  * Chart Type:**Column</em>

* **New customers by coupon / non-coupon acquisition**
  * Metric 1:**New customers</em>
    * Add filter:
      * [A] `Customer's first order's coupon_code` **IS NOT** `[NULL]`

    * Rename: *Coupon acquisition customer*

  * Metric 2:**New customers</em>
    * Add filter:
      * [A] `coupon_code` **IS**`[NULL]`

    * Rename: *Non-coupon acquisition customer*

  * Time period:**All time</em>
  * Interval:**By Month</em>
  * Chart Type:**Stacked Column</em>

After building the reports, refer to the image at the top of this topic for how you can organize the reports on your dashboard.
