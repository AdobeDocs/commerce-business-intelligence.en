---
title: Marketing ROI
description: Learn how to set up a dashboard that track your channel analysis – including ROI in aggregate and by campaign.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
TQID: https://experienceleague.adobe.com/TJ0KsU551M5PkQcY-Ic0PuExtC9SCkO0MhZGdHL4N6g
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
---
# Marketing ROI

>[!NOTE]
>
>This topic contains instructions for clients that are using the original architecture and new architecture. You are on the [new architecture](../../administrator/account-management/new-architecture.md) if you have the "Data Warehouse Views" section available after selecting "Manage Data" from the main toolbar.

If you are spending money on online advertising, you want to track your return on this spend and make data-driven decisions on further investments. This topic demonstrates how to set up a dashboard that track your channel analysis – including ROI in aggregate and by campaign.

![Marketing dashboard showing ROI metrics and campaign performance](../../assets/Marketing_dashboard_example.png)

Before getting started, you want to connect your [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md), and [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) accounts and bring in any additional online ad spend data. This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Consolidated Tables

**Original architecture:** To bring together your spend from various sources, like [!DNL Facebook Ads] or [!DNL Google Adwords], Adobe recommends creating a **consolidated table** of all of your ad spend. You need an analyst to complete this step for you. If you have not, [file a support request](../../guide-overview.md#Submitting-a-Support-Ticket) with the subject `[MARKETING ROI ANALYSIS]`, and an analyst creates this table.

**New architecture:** You can follow the example in [this Analysis Library](../../data-analyst/data-warehouse-mgr/create-dw-views.md) topic. Consolidated Tables are now known as Data Warehouse Views on the new architecture.

## Calculated Columns

Columns to create

* **`Consolidated Digital Ad Spend`** table
* **`Campaign name`** is created by an Adobe analyst as part of your **[MARKETING ROI ANALYSIS]** ticket 

**Original and new architectures:**

* **`sales_flat_order`** table
  * **`Order's GA campaign`**
    * Select a definition: `Joined Column`
    * [!UICONTROL Create Path]:
    * [!UICONTROL Many]: `sales_flat_order.increment_id`
    * [!UICONTROL One]: `ecommerce####.transaction_id`

    * Select a [!UICONTROL table]: `ecommerce####`
    * Select a [!UICONTROL column]: `campaign`
    * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`

  * **`Order's GA medium`**
    * Select a definition: Joined Column
    * Select a [!UICONTROL table]: `ecommerce####`
    * Select a [!UICONTROL column]: `medium`
    * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce#####.transactionId

  * **`Order's GA source`**
    * Select a definition: Joined Column
    * Select a [!UICONTROL table]: `ecommerce####`
    * Select a [!UICONTROL column]: `source`
    * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce#####.transactionId
^

* **`customer_entity`** table
* **`Customer's first order GA campaign`**
  * Select a definition: `Max`
  * Select a [!UICONTROL table]: `sales_flat_order`
  * Select a [!UICONTROL column]: `Order's GA campaign`
  * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
  * [!UICONTROL Filter]:
    * `Orders we count`
    * `Customer's order number = 1`

* **`Customer's first order GA source`**
  * Select a definition: `Max`
  * Select a [!UICONTROL table]: `sales_flat_order`
  * Select a [!UICONTROL column]: `Order's GA source`
  * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
  * [!UICONTROL Filter]:
    * `Orders we count`
    * `Customer's order number = 1`

* **`Customer's first order GA medium`**
  * Select a definition: `Max`
  * Select a [!UICONTROL table]: `sales_flat_order`
  * Select a [!UICONTROL column]: `Order's GA medium`
  * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
  * [!UICONTROL Filter]:
    * `Orders we count`
    * `Customer's order number = 1`

* **`sales_flat_order`** table
* **`Customer's first order GA campaign`**
  * Select a definition: `Joined Column`
  * Select a [!UICONTROL table]: `customer_entity`
  * Select a [!UICONTROL column]: `Customer's first order GA campaign`
  * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
  * Select a definition: Joined Column
  * Select a [!UICONTROL table]: `customer_entity`
  * Select a [!UICONTROL column]: `Customer's first order GA source`
  * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
  * Select a definition: `Joined Column`
  * Select a [!UICONTROL table]: `customer_entity`
  * Select a [!UICONTROL column]: `Customer's first order GA medium`
  * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Metrics

* **Ad spend**
* In the **`Consolidated Digital Ad Spend`** table
* This metric performs a **Sum**
* On the **`adCost`** column
* Ordered by the **`date`** timestamp

* **Ad impressions**
* In the **`Consolidated Digital Ad Spend`** table
* This metric performs a **Sum**
* On the **`Impressions`** column
* Ordered by the **`Month`** timestamp

* **Ad clicks**
* In the **`Consolidated Digital Ad Spend`** table
* This metric performs a **Sum**
* On the **`adClicks`** column
* Ordered by the **`Month`** timestamp

>[!NOTE]
>
>Make sure to [add all new columns as dimensions to metrics](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **Ad spend (all time)**
  * [!UICONTROL Metric]: Ad Spend

* Metric `A`: Ad Spend
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Scalar`

* **Ad customer acquisitions (all time)**
  * [!UICONTROL Metric]: `New customers`
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * Filter logic: ([`A`] OR [`B`] OR [`C`]) AND [`D`]

* Metric `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Scalar`

* **Ad ROI**
  * [!UICONTROL Metric]: Ad Spend

  * [!UICONTROL Metric]: `New customers`
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * Filter logic: ([`A`] OR [`B`] OR [`C`]) AND [`D`]

  * [!UICONTROL Metric]: Average lifetime revenue
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * Filter logic: ([`A`] OR [`B`] OR [`C`]) AND [`D`]

  * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
  * [!UICONTROL Format]: `Percentage`

* Metric `A`: `Ad Spend (hide)`
* Metric `B`: `Ad customer acquisitions (hide)`
* Metric `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Chart Type]: `Scalar`

* **Orders by ga medium**
  * [!UICONTROL Metric]: `Orders`

* Metric `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* [!UICONTROL Chart Type]: `Area`

* **Ad ROI by campaign**
  * [!UICONTROL Metric]: `Ad Spend`

  * [!UICONTROL Metric]:`New customers`
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * Filter logic: ([`A`] OR [`B`] OR [`C`]) AND [`D`]

  * [!UICONTROL Metric]: Average lifetime revenue
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * Filter logic: ([`A`] OR [`B`] OR [`C`]) AND [`D`]

  * [!UICONTROL Metric]: Average lifetime number of orders
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * Filter logic: ([`A`] OR [`B`] OR [`C`]) AND [`D`]

  * [!UICONTROL Formula]: `(A / B)`
  * [!UICONTROL Format]: `Currency`

  * [!UICONTROL Formula]: `(C - (A / B))`
  * [!UICONTROL Format]: `Currency`

  * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
  * [!UICONTROL Format]: `Percentage`

  * [!UICONTROL Metric]: `Ad Clicks`

  * [!UICONTROL Metric]: `Ad Impressions`

  * [!UICONTROL Formula]: `(H / I)`
  * [!UICONTROL Format]: `Percentage`

  * [!UICONTROL Formula]: `(A / H)`
  * [!UICONTROL Format]: `Currency`

* Metric `A`: `Ad Spend` (hide)
* Metric `B`: `Ad customer acquisitions`
* Metric `C`: `Average LTV`
* Metric `D`: `Average lifetime # of orders`
* [!UICONTROL Formula]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Metric `H`: `adClicks`
* Metric `I`: `Impressions`
* [!UICONTROL Formula]: `CTR`
* [!UICONTROL Formula]: `CPC`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `campaign` (Use `Customer's first order's` campaign for non-ad spend table metrics)
* [!UICONTROL Chart Type]: `Table`

If you run into any questions while building this analysis, or simply want to engage the Professional Services team, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### Related

* [Best-Practices for UTM tagging in [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [How does [!DNL Google Analytics] UTM attribution work?](../analysis/utm-attributes.md)
