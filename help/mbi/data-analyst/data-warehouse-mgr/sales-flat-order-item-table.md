---
title: sales_order_item table
description: Learn how to work with the sales_order_item table.
---
# `sales_order_item` Table

The `sales_order_item` table (`sales_flat_order_item` on [!DNL Magento] 1) contains records of all products that were purchased in an order. Each row represents a unique `sku` included in an order. The quantity of units that were purchased for a specific `sku` is most often represented by the `qty_ordered` field.

## Product Types

The `sales_order_item` captures details on all [product types](https://docs.magento.com/m2/ce/user_guide/catalog/product-types.html) that were purchased. A common practice in **[!UICONTROL Magento]** is to offer configurable products, or in other words, a product that can be customized according to size, color, and other product attributes. Although a configurable product has its own `sku`, it can relate to multiple simple products, where each simple product represents a unique product configuration. Refer to [configuring products](https://devdocs.magento.com/guides/v2.3/rest/tutorials/configurable-product/config-product-intro.html) for more information.

For example, consider a configurable product such as a t-shirt. When a customer checks out, they select options to alter the color and size. If the customer selects a color of `blue`, and a size of `small`, they end up purchasing a simple product like `t-shirt-blue-small` which relates back to the parent product of `t-shirt`.

When a configurable product is included in an order, two rows are generated in the `sales_order_item` table: one for the [simple](https://docs.magento.com/m2/ce/user_guide/catalog/product-create-simple.html) `sku`, and one for the [configurable](https://docs.magento.com/m2/ce/user_guide/catalog/product-create-configurable.html) parent. These two records in the `sales_order_item` table can be related to each other through the following join:

*  (simple) `sales_order_item.parent_item_id` => (configurable) `sales_order_item.item_id`

Therefore it is possible to report on sales of products either at the simple level or at the configurable level. By default, all standard `order-item-level` metrics in [!DNL MBI] are configured to exclude the simple products, and *only* report on the configurable versions. This is accomplished through the `Ordered products we count` filter set, which filters on the condition where `parent_item_id` is `NULL`.

## Common Columns

|**Column Name**|**Description**|
|----|----|
|`base_price`|Price of an individual unit of a product at the time of sale after [catalog price rules, tiered discounts, and special pricing](https://docs.magento.com/m2/ce/user_guide/catalog/pricing-advanced.html) are applied and before any taxes, shipping, or cart discounts are applied, represented in the base currency of the store|
|`created_at`|Creation timestamp of the order item, usually stored locally in UTC. Depending on your configuration in [!DNL MBI], this timestamp may be converted to a reporting time zone in [!DNL MBI] that differs from your database time zone|
|`item_id` (PK)|Unique identifier for the table|
|`name`|Text name of the order item|
|`order_id`|`Foreign key` associated with the `sales_order` table. Join to `sales_order.entity_id` to determine order attributes associated with the order item|
|`parent_item_id`|`Foreign key` that relates a simple product to its parent bundle or configurable product. Join to `sales_order_item.item_id` to determine parent product attributes associated with simple product. For parent order items (that is, bundle or configurable product types), the `parent_item_id` will be `NULL`|
|`product_id`|`Foreign key` associated with the `catalog_product_entity` table. Join to `catalog_product_entity.entity_id` to determine product attributes associated with the order item|
|`product_type`|Type of product that was sold. Potential [product types](https://docs.magento.com/m2/ce/user_guide/catalog/product-types.html) include: simple, configurable, grouped, virtual, bundle, and downloadable|
|`qty_ordered`|Quantity of units included in the cart for the particular order item at the time of sale|
|`sku`|Unique identifier for the order item that was purchased|
|`store_id`|`Foreign key` associated with the `store` table. Join to `store.store_id` to determine which **[!UICONTROL Magento]** store view is associated with the order item|

{style="table-layout:auto"}

## Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|`Customer's email`|Email address of the customer placing the order. Calculated by joining `sales_order_item.order_id` to `sales_order.entity_id` and returning the `customer_email` field|
|`Customer's lifetime number of orders`|Total count of orders placed by this customer. Calculated by joining `sales_order_item.order_id` to `sales_order.entity_id` and returning the `Customer's lifetime number of orders` field|
|`Customer's lifetime revenue`|Sum total of revenue for all orders placed by this customer. Calculated by joining `sales_order_item.order_id` to `sales_order.entity_id` and returning the `Customer's lifetime revenue` field|
|`Customer's order number`|Sequential order rank for this customer's order. Calculated by joining `sales_order_item.order_id` to `sales_order.entity_id` and returning the `Customer's order number` field|
|`Order item total value (quantity * price)`|Total value of an order item at the time of sale after [catalog price rules, tiered discounts, and special pricing](https://docs.magento.com/m2/ce/user_guide/catalog/pricing-advanced.html) are applied and before any taxes, shipping, or cart discounts are applied. Calculated by multiplying the `qty_ordered` by the `base_price`|
|`Order's coupon_code`|Coupon applied to the order. Calculated by joining `sales_order_item.order_id` to `sales_order.entity_id` and returning the `coupon_code` field|
|`Order's increment_id`|Unique identifier of the order. Calculated by joining `sales_order_item.order_id` to `sales_order.entity_id` and returning the `increment_id` field|
|`Order's status`|Status of the order. Calculated by joining `sales_order_item.order_id` to `sales_order.entity_id` and returning the `status` field|
|`Store name`|Name of the **[!UICONTROL Magento]** store associated with the order item. Calculated by joining `sales_order_item.store_id` to `store.store_id` and returning the `name` field|

{style="table-layout:auto"}

## Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|`Products ordered`|The total quantity of products included in carts at the time of sale|`Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at`|
|`Revenue by products ordered`|Total value of products included in carts at the time of sale after catalog price rules, tiered discounts, and special pricing are applied and before any taxes, shipping, or cart discounts are applied|`Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at`|

{style="table-layout:auto"}

## `Foreign Key` Joining Paths

`catalog_product_entity`

*  Join to `catalog_product_entity` table to create new columns that return product attributes associated with the order item.
   *  Path: `sales_order_item.product_id` (many) => `catalog_product_entity.entity_id` (one)

`sales_order`

*  Join to `sales_order` table to create new order-level columns associated with the order item.
   *  Path: `sales_order_item.order_id` (many) => `sales_order.entity_id` (one)

`sales_order_item`

*  Join to `sales_order_item` to create new columns that associate details of the parent configurable or bundle SKU with the simple product. Note that you will need to [contact support](../../getting-started/support.md) for assistance in configuring these calculations, if building in the Data Warehouse manager.
   *  Path: `sales_order_item.parent_item_id` (many) => `sales_order_item.item_id` (one)

`store`

*  Join to `store` table to create new columns that return details related to the **[!UICONTROL Magento]** store associated with the order item.
   *  Path: `sales_order_item.store_id` (many) => `store.store_id` (one)
