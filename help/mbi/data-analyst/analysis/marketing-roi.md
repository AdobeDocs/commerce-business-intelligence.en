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

Before getting started, you want to connect your [Facebook Ads](../importing-data/integrations/facebook-ads.md), [Adwords](../importing-data/integrations/google-adwords.md), and [Google Ecommerce](../importing-data/integrations/google-ecommerce.md) accounts as well as bring in any additional online ad spend data. This analysis contains [advanced calculated columns](../data-warehouse-mgr/adv-calc-columns.md).

## Consolidated Tables

**Original architecture:** In order to bring together your spend from various sources (like Facebook Ads or Google Adwords), we recommend creating a **consolidated table** of all of your ad spend. You will need an analyst to complete this step for you. If you have not already, [file a support request](../../getting-started/support.md) with the subject **[MARKETING ROI ANALYSIS]**, and an analyst will create this table.

**New architecture:** You can follow the example set forth in [this Analysis Library](../../data-analyst/data-warehouse-mgr/create-dw-views.md) topic. Consolidated Tables are now known as Data Warehouse Views on the new architecture.

## Calculated Columns

Columns to create

* <!--<span class="wysiwyg-color-blue">-->**`Consolidated Digital Ad Spend`**<!--</span>--> table
* <!--<span class="wysiwyg-color-blue">-->**`Campaign name`**<!--</span>--> will be created by an analyst as part of your **[MARKETING ROI ANALYSIS]** ticket (**note:** see above for new architecture differences)
<!--{: style="list-style-type: circle;"}-->

**Original and new architectures:**

* <!--<span class="wysiwyg-color-blue">-->**`sales_flat_order`**<!--</span>--> table
  * <!--<span class="wysiwyg-color-blue">-->**`Order's GA campaign`**<!--</span>-->
    * Select a definition: Joined Column
    * Create Path:
    * Many: sales_flat_order.increment_id
    * One: ecommerce####.transaction_id

    * Select table: <!--<span class="wysiwyg-color-blue">-->**`ecommerce####`**<!--</span>-->
    * Select column: <!--<span class="wysiwyg-color-blue">-->**`campaign`**<!--</span>-->
    * Path: sales_flat_order.increment_id = ecommerce#####.transactionId
    <!--{: style="list-style-type: square;"}-->

  * <!--<span class="wysiwyg-color-blue">-->**`Order's GA medium`**<!--</span>-->
    * Select a definition: Joined Column
    * Select table: <!--<span class="wysiwyg-color-blue">-->**`ecommerce####`**<!--</span>-->
    * Select column: <!--<span class="wysiwyg-color-blue">-->**`medium`**<!--</span>-->
    * Path: sales_flat_order.increment_id = ecommerce#####.transactionId

  * <!--<span class="wysiwyg-color-blue">-->**`Order's GA source`**<!--</span>-->
    * Select a definition: Joined Column
    * Select table: <!--<span class="wysiwyg-color-blue">-->**`ecommerce####`**<!--</span>-->
    * Select column: <!--<span class="wysiwyg-color-blue">-->**`source`**<!--</span>-->
    * Path: sales_flat_order.increment_id = ecommerce#####.transactionId
^

* <!--<span class="wysiwyg-color-blue">-->**`customer_entity`**<!--</span>--> table
* <!--<span class="wysiwyg-color-blue">-->**`Customer's first order GA campaign`**<!--</span>-->
  * Select a definition: Max
  * Select table: <!--<span class="wysiwyg-color-blue">-->**`sales_flat_order`**<!--</span>-->
  * Select column: <!--<span class="wysiwyg-color-blue">-->**`Order's GA campaign`**<!--</span>-->
  * Path: sales_flat_order.customer_id = customer_entity.entity_id
  * Filter:
  * Orders we count
  * Customer's order number = 1
  <!--{: style="list-style-type: square;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`Customer's first order GA source`**<!--</span>-->
  * Select a definition: Max
  * Select table: <!--<span class="wysiwyg-color-blue">-->**`sales_flat_order`**<!--</span>-->
  * Select column: <!--<span class="wysiwyg-color-blue">-->**`Order's GA source`**<!--</span>-->
  * Path: sales_flat_order.customer_id = customer_entity.entity_id
  * Filter:
    * Orders we count
    * Customer's order number = 1<!--<span class="wysiwyg-color-blue">-->**``**<!--</span>-->
    <!--{: style="list-style-type: circle;"}-->
  <!--{: style="list-style-type: circle;"}-->
<!--{: style="list-style-type: circle;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`Customer's first order GA medium`**<!--</span>-->
  * Select a definition: Max
  * Select table: <!--<span class="wysiwyg-color-blue">-->**`sales_flat_order`**<!--</span>-->
  * Select column: <!--<span class="wysiwyg-color-blue">-->**`Order's GA medium`**<!--</span>-->
  * Path: sales_flat_order.customer_id = customer_entity.entity_id
  * Filter:
    * Orders we count
    * Customer's order number = 1
    <!--{: style="list-style-type: circle;"}-->
  <!--{: style="list-style-type: circle;"}-->
<!--{: style="list-style-type: circle;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`sales_flat_order`**<!--</span>--> table
* <!--<span class="wysiwyg-color-blue">-->**`Customer's first order GA campaign`**<!--</span>-->
  * Select a definition: Joined Column
  * Select table: <!--<span class="wysiwyg-color-blue">-->**`customer_entity`**<!--</span>-->
  * Select column: <!--<span class="wysiwyg-color-blue">-->**`Customer's first order GA campaign`**<!--</span>-->
  * Path: sales_flat_order.customer_id = customer_entity.entity_id
  <!--{: style="list-style-type: circle;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`Customer's first order GA source`**<!--</span>-->
  * Select a definition: Joined Column
  * Select table: <!--<span class="wysiwyg-color-blue">-->**`customer_entity`**<!--</span>-->
  * Select column: <!--<span class="wysiwyg-color-blue">-->**`Customer's first order GA source`**<!--</span>-->
  * Path: sales_flat_order.customer_id = customer_entity.entity_id
  <!--{: style="list-style-type: circle;"}-->

* <!--<span class="wysiwyg-color-blue">-->**`Customer's first order GA medium`**<!--</span>-->
  * Select a definition: Joined Column
  * Select table: <!--<span class="wysiwyg-color-blue">-->**`customer_entity`**<!--</span>-->
  * Select column: <!--<span class="wysiwyg-color-blue">-->**`Customer's first order GA medium`**<!--</span>-->
  * Path: sales_flat_order.customer_id = customer_entity.entity_id
  <!--{: style="list-style-type: circle;"}-->
<!--{: style="list-style-type: circle;"}-->

## Metrics

* **Ad spend**
* In the <!--<span class="wysiwyg-color-blue">-->**`Consolidated Digital Ad Spend`**<!--</span>--> table
* This metric performs a **Sum**
* On the <!--<span class="wysiwyg-color-blue">-->**`adCost`**<!--</span>--> column
* Ordered by the <!--<span class="wysiwyg-color-blue">-->**`date`**<!--</span>--> timestamp
<!--{: style="list-style-type: circle;"}-->

* **Ad impressions**
* In the <!--<span class="wysiwyg-color-blue">-->**`Consolidated Digital Ad Spend`**<!--</span>--> table
* This metric performs a **Sum**
* On the <!--<span class="wysiwyg-color-blue">-->**`Impressions`**<!--</span>--> column
* Ordered by the <!--<span class="wysiwyg-color-blue">-->**`Month`**<!--</span>--> timestamp
<!--{: style="list-style-type: circle;"}-->

* **Ad clicks**
* In the <!--<span class="wysiwyg-color-blue">-->**`Consolidated Digital Ad Spend`**<!--</span>--> table
* This metric performs a **Sum**
* On the <!--<span class="wysiwyg-color-blue">-->**`adClicks`**<!--</span>--> column
* Ordered by the <!--<span class="wysiwyg-color-blue">-->**`Month`**<!--</span>--> timestamp
<!--{: style="list-style-type: circle;"}-->

Note: Make sure to [add all new columns as dimensions to metrics](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) before building new reports.

## Reports

* **Ad spend (all time)**
  * Metric: Ad Spend
  <!--{: style="list-style-type: square;"}-->

* *Metric A: Ad Spend*
* *Time period: All time*
* *Interval: None*
* *Chart Type: Scalar*
<!--{: style="list-style-type: circle;"}-->

* **Ad customer acquisitions (all time)**
  * Metric: New customers
  * Filters:
  * User's first order's source LIKE %google%
  * User's first order's source LIKE %facebook%
  * User's first order's source LIKE %fb%
  * User's first order's medium IN cpc, ppc
  * Filter logic: ([A] OR [B] OR [C]) AND [D]
  <!--{: style="list-style-type: square;"}-->

* *Metric A: Ad customer acquisitions*
* *Time period: All time*
* *Interval: None*
* *Chart Type: Scalar*
<!--{: style="list-style-type: circle;"}-->

* **Ad ROI**
  * Metric: Ad Spend
  <!--{: style="list-style-type: square;"}-->

  * Metric: New customers
  * Filters:
  * User's first order's source LIKE %google%
  * User's first order's source LIKE %facebook%
  * User's first order's source LIKE %fb%
  * User's first order's medium IN cpc, ppc
  * Filter logic: ([A] OR [B] OR [C]) AND [D]
  <!--{: style="list-style-type: square;"}-->

  * Metric: Average lifetime revenue
  * Filters:
  * User's first order's source LIKE %google%
  * User's first order's source LIKE %facebook%
  * User's first order's source LIKE %fb%
  * User's first order's medium IN cpc, ppc
  * Filter logic: ([A] OR [B] OR [C]) AND [D]
  <!--{: style="list-style-type: square;"}-->

  * Formula: ((C - (A / B)) / (A / B))
  * Format: Percentage
  <!--{: style="list-style-type: square;"}-->

* *Metric A: Ad Spend* (hide)
* *Metric B: Ad customer acquisitions* (hide)
* *Metric C: Average LTV* (hide)
* *Formula: Ads ROI*
* *Time period: All time*
* *Interval: None*
* *Chart Type: Scalar*
<!--{: style="list-style-type: circle;"}-->

* **Orders by ga medium**
  * Metric: Orders
  <!--{: style="list-style-type: square;"}-->

* *Metric A: Orders*
* *Time period: All time*
* *Interval: By Month*
* *Group by: **`Order's medium`***
* *Chart Type: Area chart*
<!--{: style="list-style-type: circle;"}-->

* **Ad ROI by campaign**
  * Metric: Ad Spend
  <!--{: style="list-style-type: square;"}-->

  * Metric: New customers
  * Filters:
  * User's first order's source LIKE %google%
  * User's first order's source LIKE %facebook%
  * User's first order's source LIKE %fb%
  * User's first order's medium IN cpc, ppc
  * Filter logic: ([A] OR [B] OR [C]) AND [D]
  <!--{: style="list-style-type: square;"}-->

  * Metric: Average lifetime revenue
  * Filters:
  * User's first order's source LIKE %google%
  * User's first order's source LIKE %facebook%
  * User's first order's source LIKE %fb%
  * User's first order's medium IN cpc, ppc
  * Filter logic: ([A] OR [B] OR [C]) AND [D]
  <!--{: style="list-style-type: square;"}-->

  * Metric: Average lifetime number of orders
  * Filters:
  * User's first order's source LIKE %google%
  * User's first order's source LIKE %facebook%
  * User's first order's source LIKE %fb%
  * User's first order's medium IN cpc, ppc
  * Filter logic: ([A] OR [B] OR [C]) AND [D]
  <!--{: style="list-style-type: square;"}-->

  * Formula: (A / B)
  * Format: Currency
  <!--{: style="list-style-type: square;"}-->

  * Formula: (C - (A / B))
  * Format: Currency
  <!--{: style="list-style-type: square;"}-->

  * Formula: ((C - (A / B)) / (A / B))
  * Format: Percentage
  <!--{: style="list-style-type: square;"}-->

  * Metric: Ad Clicks
  <!--{: style="list-style-type: square;"}-->

  * Metric: Ad Impressions
  <!--{: style="list-style-type: square;"}-->

  * Formula: (H / I)
  * Format: Percentage
  <!--{: style="list-style-type: square;"}-->

  * Formula: (A / H)
  * Format: Currency
  <!--{: style="list-style-type: square;"}-->

* *Metric A: Ad Spend* (hide)
* *Metric B: Ad customer acquisitions*
* *Metric C: Average LTV*
* *Metric D: Average lifetime # of orders*
* *Formula: CAC*
* *Formula: Avg return*
* *Formula: Ads ROI*
* *Metric H: adClicks*
* *Metric I: Impressions*
* *Formula: CTR*
* *Formula: CPC*
* *Time period: All time*
* *Interval: None*
* *Group by: **`campaign`** (Use Customer's first order's campaign for non-ad spend table metrics)*
* *Chart Type: Table*
<!--{: style="list-style-type: circle;"}-->

If you run into any questions while building this analysis, or simply want to engage our professional services team, [contact support](../../getting-started/support.md).

### Related Reading

* [Best-Practices for UTM tagging in Google Analytics](../../best-practices/utm-tagging-google.md)
* [How does Google Analytics UTM attribution work?](../analysis/utm-attributes.md)
