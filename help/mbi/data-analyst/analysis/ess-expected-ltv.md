---
title: Expected Lifetime Value (LTV) Analysis (basic)
zendesk_id: 360016729711
---

Forecasting the lifetime value of customers as they place more orders is one of the most important aspects of any business of any size.

Here are the steps to create analyses to understand your current customers' lifetime value, and forecast how lifetime value will increase with more orders:

![expected lifetime value](../../assets/expected_ltv_720.png)

#### Building a Metric

The first step will be to construct a new metric with the following steps:
* Navigate to **Manage Data &gt; Metrics**
  * View the existing **Avg lifetime revenue** Note the table this metric is constructed on (probably `customer_entity` or `sales_order` depending on your store's ability to accept guest checkout!).
  * Click **Create New Metric **and select the table from above.
  * This metric performs a **Median** on the **Customer's lifetime revenue **column, ordered by **created_at**.
    * FILTERS:
      * Add the **Customers we count (Saved Filter Set)** (or **Registered accounts we count**)

  * Give the metric a name, such as **Median lifetime revenue**.

#### Creating your Dashboard

Once the metric has been created, you can **create a dashboard** by doing this:
* Navigate to **Dashboards &gt; Dashboard Options &gt; Create New Dashboard.**
* Give the dashboard a name such as **Expected LTV**.

* This will be where we create and add all the reports.

#### Building Reports

* If you have not already, check out [this video](https://fast.wistia.net/embed/iframe/24zz7wmjrt) about using the Visual Report Builder to build charts, tables, and scalar values.
* Note on **Time Period:** The time period for each report is listed as "All-time". Please feel free to alter this to suit your analysis needs. We recommend all reports on this dashboard cover the same time period, such as "All time", "Year-to-date", or "Last 365 days".

* **Average LTV (all)**
  * <em>Metric:</em> Avg lifetime revenue
  * <em>Time period:</em> All time
  * <em>Interval:</em> None
  * *Chart Type:* Number (scalar)

* **Average LTV (customers / non-guest checkout)**
  * <em>Metric:</em> Avg lifetime revenue
    * Add filters:
      * [A] `Customer's group code` **Not Equal To** `Not Logged In`
      * [B] `Customer's lifetime number of orders` **Greater Than**`0`

  * <em>Time period: </em>All time
  * <em>Interval: </em>None
  * <em>Chart Type: </em>Number (scalar)

* **Average and Median LTV**
  * <em>Metric 1: </em>Avg lifetime revenue
  * <em>Metric 2: </em>Median lifetime revenue
  * <em>Time period: </em>All time
  * <em>Interval: </em>By Month
  * <em>Chart Type: </em>Line
  * <em>Uncheck </em>**Multiple Y-Axes**

* **LTV by lifetime number of orders**
  * <em>Metric 1: </em>Avg lifetime revenue
  * <em>Metric 2: </em>New customers
  * <em>Time period: </em>All time
  * <em>Interval: </em>None
  * <em>Group by: </em>Customer's lifetime number of orders
  * <em>Chart Type: </em>Line
  * <em>Note: </em>
    * Do not add all of the values for "Customer's lifetime number of orders", instead look at a point where the number of New Customers reaches a small number, and manually add each Customer's lifetime number of order value to that point. For instance, if there are 200 customers at one order, 75 at two, 15 at three, and 3 at four, add **1, 2, and 3**.

* Add the existing **Avg customer lifetime revenue by cohort** report

After building the reports, refer to the image at the top of this topic for how you can organize the reports on your dashboard.
