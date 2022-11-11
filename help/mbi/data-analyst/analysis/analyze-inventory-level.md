---
title: Analyzing Inventory Levels
description: Learn how to analyze inventory levels.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
---
# Analyze Inventory Levels

This topic demonstrates how to set up a dashboard which will provide insights into your current inventory. This topic contains instructions for clients on both the legacy architecture or new architecture. You are on the legacy architecture if you do not have the **[!UICONTROL Data Warehouse Views]** option under the **[!UICONTROL Manage Data]** menu). If you are on the legacy architecture, submit a [new support request](../../guide-overview.md) with the subject **[!UICONTROL INVENTORY ANALYSIS]** once you reach the designated section in the _Calculated columns_ instructions below.

## Columns to track:

### Columns to track instructions

* **[!UICONTROL cataloginventory_stock_item]** table:
  * **`item_id`**
  * **`product_id`**
  * **`qty`**

* **[!UICONTROL catalog_product_entity]** table:
  * **`entity_id`**
  * **`sku`**
  * **`created_at`**

## Calculated columns:

### New Architecture

* **[!UICONTROL catalog_product_entity]** table:
  * **`Product's most recent order date`**
    * [!UICONTROL Column type]: `Many to One`
    * [!UICONTROL Column equation]: `MAX`
    * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `created_at`
    * [!UICONTROL Filters]:
      * [A] `Ordered products we count`

  * **`Product's first order date`**
    * [!UICONTROL Column type]: `Many to One`
    * [!UICONTROL Column equation]: `MIN`
    * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `created_at`
    * [!UICONTROL Filters]:
      * [A] `Ordered products we count`

  * **`Seconds since product's most recent order date`**
    * [!UICONTROL Column type]: `Same Table`
    * [!UICONTROL Column equation]: `AGE`
    * Select [!UICONTROL DATETIME column]: `Product's most recent order date`

  * **`Product's lifetime number of items sold`**
    * [!UICONTROL Column type]: `Many to One`
    * [!UICONTROL Column equation]: `SUM`
    * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `qty_ordered`
    * [!UICONTROL Filters]:
      * [A] `Ordered products we count`

  * **`Avg products sold per week (all time)`**
    * [!UICONTROL Column type]: `Same Table`
    * [!UICONTROL Column equation]: `CALCULATION`
    * [!UICONTROL Column] inputs:
      * A: `Product's lifetime number of items sold`
      * B: `Product's first order date`
    * [!UICONTROL Datatype]: `Decimal`
    * Definition:
      * case when A is null or B is null then null else round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) end

* **[!UICONTROL cataloginventory_stock_item]** table:
  * **`Sku`**
    * [!UICONTROL Column type]: `One to Many`
    * [!UICONTROL Column equation]: `JOINED_COLUMN`
    * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `sku`

  * **`Product's lifetime number of items sold`**
    * [!UICONTROL Column type]: `One to Many`
    * [!UICONTROL Column equation]: `JOINED_COLUMN`
    * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `Product's lifetime number of items sold`

  * **`Seconds since product's most recent order date`**
    * [!UICONTROL Column type]: `One to Many`
    * [!UICONTROL Column equation]: `JOINED_COLUMN`
    * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `Seconds since product's most recent order date`

  * **`Avg products sold per week (all time)`**
    * [!UICONTROL Column type]: `One to Many`
    * [!UICONTROL Column equation]: `JOINED_COLUMN`
    * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `Avg products sold per week (all time)`

  * **`Weeks on hand`**
    * [!UICONTROL Column type]: `Same Table`
    * [!UICONTROL Column equation]: `CALCULATION`
    * [!UICONTROL Column] inputs:
      * A: `qty`
      * B: `Avg products sold per week (all time)`
    * [!UICONTROL Datatype]: `Decimal`
    * Definition:
      * case when A is null or B is null or B = 0.0 then null else round(A::decimal/B,2) end

### Legacy Architecture

* **[!UICONTROL catalog_product_entity]** table:
  * **`Product's most recent order date`**
    * [!UICONTROL Column type]: `Many to One`
    * [!UICONTROL Column equation]: `MAX`
    * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `created_at`
    * [!UICONTROL Filters]:
      * [A] `Ordered products we count`

  * **`Product's first order date`**
    * [!UICONTROL Column type]: `Many to One`
    * [!UICONTROL Column equation]: `MIN`
    * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `created_at`
    * [!UICONTROL Filters]:
      * [A] `Ordered products we count`

  * **`Seconds since product's most recent order date`**
    * [!UICONTROL Column type]: `Same Table`
    * [!UICONTROL Column equation]: `AGE`
    * Select DATETIME column: **`Product's most recent order date`**

  * **`Product's lifetime number of items sold`**
    * [!UICONTROL Column type]: `Many to One`
    * [!UICONTROL Column equation]: `SUM`
    * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
    * Select a [!UICONTROL column]: **`qty_ordered`**
    * [!UICONTROL Filters]:
      * [A] `Ordered products we count`

  * **`Avg products sold per week (all time)`**
    * Will be created by an analyst when you file submit your **[INVENTORY ANALYSIS]** support request

* **[!UICONTROL cataloginventory_stock_item]** table:
  * **`Sku`**
    * [!UICONTROL Column type]: `One to Many`
    * [!UICONTROL Column equation]: `JOINED_COLUMN`
    * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `sku`

  * **`Product's lifetime number of items sold`**
    * [!UICONTROL Column type]: `One to Many`
    * [!UICONTROL Column equation]: `JOINED_COLUMN`
    * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `Product's lifetime number of items sold`

  * **`Seconds since product's most recent order date`**
    * [!UICONTROL Column type]: `One to Many`
    * [!UICONTROL Column equation]: `JOINED_COLUMN`
    * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `Seconds since product's most recent order date`

  * **`Avg products sold per week (all time)`**
    * [!UICONTROL Column type]: `One to Many`
    * [!UICONTROL Column equation]: `JOINED_COLUMN`
    * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
    * Select a [!UICONTROL column]: `Avg products sold per week (all time)`

  * **`Weeks on hand`**
    * Will be created by an analyst when you file submit your **[!UICONTROL INVENTORY ANALYSIS]** support request

## Metrics

### Metrics instructions

* **[!UICONTROL cataloginventory_stock_item]** table:
  * **`Inventory on hand`**: this metric performs a
    * **Sum** on the
    * **`qty`** column ordered by the
    * [None] column

## Reports

### Report instructions

* **`Inventory on hand by sku`**
  * [!UICONTROL Metric]: `Inventory on hand`
  * [!UICONTROL Time period]: `All time`
  * Time interval: `None`
  * [!UICONTROL Group by]:
    * `Sku`
    * `Weeks on hand`
  * [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
  * [!UICONTROL Metric]: `Inventory on hand`
    * [!UICONTROL Filters]:
      * [A] `Weeks on hand` `< 2`

  * [!UICONTROL Time period]: `All time`
  * Time interval: `None`
  * [!UICONTROL Group by]: `Sku`
  * [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
  * [!UICONTROL Metric]: `Inventory on hand`
    * [!UICONTROL Filters]:
      * [A] `Weeks on hand` `> 26` 

  * [!UICONTROL Time period]: `All time`
  * Time interval: `None`
  * [!UICONTROL Group by]: `Sku`
  * [!UICONTROL Chart type]: `Table`

If you run into any questions while building this analysis, or simply want to engage our professional services team, [contact support](../../guide-overview.md).
