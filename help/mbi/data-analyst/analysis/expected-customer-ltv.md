---
title: Expected Lifetime Value (LTV) Analysis for Pro
description: Learn how to set up a dashboard that helps you understand customer lifetime value growth and expected lifetime value of your customers.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
    internal-label: Expert
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Expected Lifetime Value Analysis

This topic demonstrates how to set up a dashboard that helps you understand customer lifetime value growth and expected lifetime value of your customers. 

![Expected lifetime value analysis dashboard showing customer value projections](../../assets/exp-lifetim-value-anyalysis.png)

This analysis is only available to Pro account customers on the new architecture. If your account has access to the `Persistent Views` feature under the `Manage Data` side bar, you are on the new architecture and can follow the instructions listed here to build this analysis yourself.

Before getting started, you want to familiarize yourself with the [cohort report builder.](../dev-reports/cohort-rpt-bldr.md)

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

After compiling all the reports, you can organize them on the dashboard as you desire. The result may look like the image at the top of the page.

If you run into any questions while building this analysis, or simply want to engage the Professional Services team, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
