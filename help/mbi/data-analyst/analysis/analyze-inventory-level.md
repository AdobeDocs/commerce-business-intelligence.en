---
title: Analyzing Inventory Levels
description: Learn how to analyze inventory levels. 
---
# Analyze Inventory Levels

This topic demonstrates how to set up a dashboard which will provide insights into your current inventory. This topic contains instructions for clients on both the legacy architecture or new architecture. You are on the legacy architecture if you do not have the **Data Warehouse Views** option under the **[!DNL Manage Data]** menu). If you are on the legacy architecture, submit a [new support request](../../getting-started/support.md) with the subject **[INVENTORY ANALYSIS]** once you reach the designated section in the "Calculated columns" instructions below.

## Columns to track:

### Columns to track instructions

* **cataloginventory_stock_item** table:
  * **`item_id`**
  * **`product_id`**
  * **`qty`**

* **catalog_product_entity** table:
  * **`entity_id`**
  * **`sku`**
  * **`created_at`**

## Calculated columns:

### New Architecture

* **catalog_product_entity** table:
  * **`Product's most recent order date`**
    * Column type: Many to One
    * Column equation: MAX
    * Path: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`created_at`**
    * Filters:
      * [A] Ordered products we count

  * **`Product's first order date`**
    * Column type: Many to One
    * Column equation: MIN
    * Path: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`created_at`**
    * Filters:
      * [A] Ordered products we count

  * **`Seconds since product's most recent order date`**
    * Column type: Same Table
    * Column equation: AGE
    * Select DATETIME column: **`Product's most recent order date`**

  * **`Product's lifetime number of items sold`**
    * **``**Column type: Many to One
    * Column equation: SUM
    * Path: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`qty_ordered`**
    * Filters:
      * [A] Ordered products we count

  * **`Avg products sold per week (all time)`**
    * Column type: Same Table
    * Column equation: CALCULATION
    * Column inputs:
      * A: **`Product's lifetime number of items sold`**
      * B: **`Product's first order date`**
    * Datatype: Decimal
    * Definition:
      * case when A is null or B is null then null else round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) end

* **cataloginventory_stock_item** table:
  * **`Sku`**
    * Column type: One to Many
    * Column equation: JOINED_COLUMN
    * Path: **`cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`sku`**

  * **`Product's lifetime number of items sold`**
    * Column type: One to Many
    * Column equation: JOINED_COLUMN
    * Path: **`cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`Product's lifetime number of items sold`**

  * **`Seconds since product's most recent order date`**
    * Column type: One to Many
    * Column equation: JOINED_COLUMN
    * Path: **`cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`Seconds since product's most recent order date`**

  * **`Avg products sold per week (all time)`**
    * Column type: One to Many
    * Column equation: JOINED_COLUMN
    * Path: **`cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`Avg products sold per week (all time)`**

  * **`Weeks on hand`**
    * Column type: Same Table
    * Column equation: CALCULATION
    * Column inputs:
      * A: **`qty`**
      * B: **`Avg products sold per week (all time)`**
    * Datatype: Decimal
    * Definition:
      * case when A is null or B is null or B = 0.0 then null else round(A::decimal/B,2) end

### Legacy Architecture

* **catalog_product_entity** table:
  * **`Product's most recent order date`**
    * Column type: Many to One
    * Column equation: MAX
    * Path: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`created_at`**
    * Filters:
      * [A] Ordered products we count

  * **`Product's first order date`**
    * Column type: Many to One
    * Column equation: MIN
    * Path: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`created_at`**
    * Filters:
      * [A] Ordered products we count

  * **`Seconds since product's most recent order date`**
    * Column type: Same Table
    * Column equation: AGE
    * Select DATETIME column: **`Product's most recent order date`**

  * **`Product's lifetime number of items sold`**
    * **``**Column type: Many to One
    * Column equation: SUM
    * Path: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`qty_ordered`**
    * Filters:
      * [A] Ordered products we count

  * **`Avg products sold per week (all time)`**
    * Will be created by an analyst when you file submit your **[INVENTORY ANALYSIS]** support request

* **cataloginventory_stock_item** table:
  * **`Sku`**
    * Column type: One to Many
    * Column equation: JOINED_COLUMN
    * Path: **`cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`sku`**

  * **`Product's lifetime number of items sold`**
    * Column type: One to Many
    * Column equation: JOINED_COLUMN
    * Path: **`cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`Product's lifetime number of items sold`**

  * **`Seconds since product's most recent order date`**
    * Column type: One to Many
    * Column equation: JOINED_COLUMN
    * Path: **`cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`Seconds since product's most recent order date`**

  * **`Avg products sold per week (all time)`**
    * Column type: One to Many
    * Column equation: JOINED_COLUMN
    * Path: **`cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`**
    * Select a column: **`Avg products sold per week (all time)`**

  * **`Weeks on hand`**
    * Will be created by an analyst when you file submit your **[INVENTORY ANALYSIS]** support request

## Metrics

### Metrics instructions

* **cataloginventory_stock_item** table:
  * **`Inventory on hand`**: this metric performs a
    * **Sum** on the
    * **`qty`** column ordered by the
    * [None] column**``**

## Reports

### Report instructions

* **`Inventory on hand by sku`**
  * Metric: **`Inventory on hand`**
  * Time period: All time
  * Time interval: None
  * Group by:
    * **`Sku`**
    * **`Weeks on hand`**
  * Chart type: Table

* **`Inventory with less than 2 weeks on hand (order now)`**
  * Metric: **`Inventory on hand`**
    * Filters:
      * [A] **`Weeks on hand`** < 2

  * Time period: All time
  * Time interval: None
  * Group by:
    * **`Sku`**
  * Chart type: Table

* **`Inventory with more than 26 weeks on hand (put on sale)`**
  * Metric: **`Inventory on hand`**
    * Filters:
      * [A] **`Weeks on hand`** > 26 

  * Time period: All time
  * Time interval: None
  * Group by:
    * **`Sku`**
  * Chart type: Table

If you run into any questions while building this analysis, or simply want to engage our professional services team, [contact support](../../getting-started/support.md).
