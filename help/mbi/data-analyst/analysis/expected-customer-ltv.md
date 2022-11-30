---
title: Expected Lifetime Value (LTV) Analysis for Pro
description: Learn how to set up a dashboard that will help you understand customer lifetime value growth and expected lifetime value of your customers.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
---
# Expected Lifetime Value Analysis

In this article, we demonstrate how to set up a dashboard that will help you understand customer lifetime value growth and expected lifetime value of your customers. 

![](../../assets/exp-lifetim-value-anyalysis.png)

This analysis is only available to Pro account customers on the new architecture. If your account has access to the `Persistent Views` feature under the `Manage Data` side bar, you are on the new architecture and can follow the instructions listed here to build this analysis yourself.

Before getting started, you will want to familiarize yourself with our [cohort report builder.](../dev-reports/cohort-rpt-bldr.md)

## Calculated Columns

Columns to create on the **orders** table if using **30-day months**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `Seconds between customer's first order date and this order`
* [!UICONTROL Datatype]: `Integer`
* **Definition:**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* [!UICONTROL Datatype]: `Integer`
* Definition: `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

Columns to create on the **`orders`** table if using **calendar** months:

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
  * `A` = `created_at`
  * `B` = `Customer's first order date`

* [!UICONTROL Datatype]: `Integer`
* Definition: `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* [!UICONTROL Datatype]: `Integer`
* **Definition:**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* [!UICONTROL Datatype]: `String`
* Definition: `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## Metrics

### Metric instructions

Metrics to create

* **Distinct customers by first order date**
  * If you enable guest orders, use `customer_email`

* In the **`orders`** table
* This metric performs a **Count Distinct Values**
* On the **`customer_id`** column
* Ordered by the **`Customer's first order date`** timestamp

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

### Report instructions

**Expected revenue per customer by month**

* Metric `A`: `Revenue (hide)`
  * `Calendar months between first order and this order` `<= X` (Pick some reasonable number for X, for example, 24 months)
  * `Is in current month?` = `No`

* [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Filter]:

* Metric `B`: `All time customers (hide)`
  * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* Metric `C`: `All time customers by month since first order (hide)`
  * `Calendar months since order` `<= X`
  * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* [!UICONTROL Format]: `Currency`

Other chart details

* [!UICONTROL Time period]: `All time`
* Time interval: `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order` - show all
* Change the `group by` for the `All time customers` metric to Independent using the pencil icon next to the `group by`
* Edit the `Show top/bottom` fields as follows:
  * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
  * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
  * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**Avg revenue per month by cohort**

* Metric `A`: `Revenue`
* [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**Cumulative avg revenue per month by cohort**

* Metric `A`: `Revenue`
* [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the image at the top of the page.

If you run into any questions while building this analysis, or simply want to engage our professional services team, [contact support](../../guide-overview.md).
