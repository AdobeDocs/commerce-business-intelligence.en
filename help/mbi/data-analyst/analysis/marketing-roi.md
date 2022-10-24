---
title: Marketing ROI
description: Learn how to set up a dashboard that will track your channel analysis – including ROI in aggregate and by campaign. 
---
# Marketing ROI

>[!NOTE]
>
>This article contains instructions for clients that are utilizing the original architecture and new architecture. You are on the [new architecture](../../administrator/account-management/new-architecture.md) if you have the "Data Warehouse Views" section available after selecting "Manage Data" from the main toolbar.

If you are spending money on online advertising, you will inevitably want to track your return on this spend and make data-driven decisions on further investments. In this article, we demonstrate how to set up a dashboard that will track your channel analysis – including ROI in aggregate and by campaign.

![](../../assets/Marketing_dashboard_example.png)

Before getting started, you want to connect your [!DNL [Facebook Ads](../importing-data/integrations/facebook-ads.md)], [!DNL [Adwords](../importing-data/integrations/google-adwords.md)], and [!DNL [Google Ecommerce](../importing-data/integrations/google-ecommerce.md)] accounts as well as bring in any additional online ad spend data. This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Consolidated Tables

**Original architecture:** To bring together your spend from various sources (like [!DNL Facebook Ads] or [!DNL Google Adwords]), we recommend creating a **consolidated table** of all of your ad spend. You will need an analyst to complete this step for you. If you have not already, [file a support request](../../getting-started/support.md) with the subject `[MARKETING ROI ANALYSIS]`, and an analyst will create this table.

**New architecture:** You can follow the example set forth in [this Analysis Library](../../data-analyst/data-warehouse-mgr/create-dw-views.md) topic. Consolidated Tables are now known as Data Warehouse Views on the new architecture.

## Calculated Columns

Columns to create

* **`Consolidated Digital Ad Spend`** table
* **`Campaign name`** will be created by an analyst as part of your **[MARKETING ROI ANALYSIS]** ticket 

>[!NOTE]
>
>See above for new architecture differences.

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

If you run into any questions while building this analysis, or simply want to engage our professional services team, [contact support](../../getting-started/support.md).

### Related

* [Best-Practices for UTM tagging in [!DNL Google Analytics](../../best-practices/utm-tagging-google.md)]
* [How does [!DNL Google Analytics] UTM attribution work?](../analysis/utm-attributes.md)
