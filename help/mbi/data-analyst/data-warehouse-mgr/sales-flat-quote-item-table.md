---
title: quote_item table
description: Learn how to work with the quote_item table.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/wLNm1g1L6-0Ded-bZT991KvJi3dVO6zA4i2qftiX2J0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# quote_item Table

The `quote_item` table (`sales_flat_quote_item` on M1) contains records on every item added to a shopping cart, whether the cart was abandoned or converted to a purchase. Each row represents one cart item. Due to the potential size of this table, Adobe recommends you periodically delete records if certain criteria are met, such as if there are any unconverted carts older than 60 days.

>[!NOTE]
>
>Analyzing historical, abandoned carts is only possible if you do not delete records from the `quote` and `quote_item` table. If you do delete records, you are only able to see the carts not yet removed from your database.

## Common Native Columns

|**Column Name**|**Description**|
|---|---|
|`base_price`|Price of an individual unit of a product at the time the item was added to a cart, after [catalog price rules, tiered discounts, and special pricing](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) are applied and before any taxes, shipping, or cart discounts are applied. This is represented in the base currency of the store.|
|`created_at`|Creation timestamp of the cart item, stored locally in UTC. Depending on your configuration in [!DNL Commerce Intelligence], this timestamp may be converted to a reporting time zone in [!DNL Commerce Intelligence] that differs from your database time zone|
|`item_id` (PK)|Unique identifier for the table|
|`name`|Text name of the order item|
|`parent_item_id`|`Foreign key` that relates a simple product to its parent bundle or configurable product. Join to `quote_item.item_id` to determine parent product attributes associated with simple product. For parent cart items (that is, bundle or configurable product types), the `parent_item_id` is `NULL`|
|`product_id`|`Foreign key` associated with the `catalog_product_entity` table. Join to `catalog_product_entity.entity_id` to determine product attributes associated with the order item|
|`product_type`|Type of product that was added to the cart. Potential [product types](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) include: simple, configurable, grouped, virtual, bundle, and downloadable|
|`qty`|Quantity of units included in the cart for the particular cart item|
|`quote_id`|`Foreign key` associated with the `quote` table. Join to `quote.entity_id` to determine cart attributes associated with the cart item|
|`sku`|Unique identifier for the cart item|
|`store_id`|Foreign key associated with the `store` table. Join to `store.store_id` to determine which Commerce store view is associated with the cart item|

{style="table-layout:auto"}

## Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|`Cart creation date`|Timestamp associated with the cart creation date. Calculated by joining `quote_item.quote_id` to `quote.entity_id` and returning the `created_at` timestamp|
|`Cart is active? (1/0)`|Boolean field that returns "1" if the cart was created by a customer and has not yet converted to an order. Returns "0" for converted carts, or carts created through the admin. Calculated by joining `quote_item.quote_id` to `quote.entity_id` and returning the `is_active` field|
|`Cart item total value (qty * base_price)`|Total value of an item at the time the item was added to a cart, after [catalog price rules, tiered discounts, and special pricing](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) are applied and before any taxes, shipping, or cart discounts are applied. Calculated by multiplying the `qty` by the `base_price`|
|`Seconds since cart creation`|Elapsed time between the cart's creation date and now. Calculated by joining `quote_item.quote_id` to `quote.entity_id` and returning the `Seconds since cart creation` field|
|`Store name`|Name of the Commerce store associated with the order item. Calculated by joining `sales_order_item.store_id` to `store.store_id` and returning the `name` field|

{style="table-layout:auto"}

## Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|`Number of abandoned cart items`|Total quantity of items added to carts that meet specific "abandonment" conditions|`Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filters:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, where "x" corresponds to the elapsed time (in seconds) since cart creation beyond which a cart is considered abandoned|
|`Abandoned cart item value`|Sum of total revenue associated with carts that meet specific "abandonment" conditions|`Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filters:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, where "x" corresponds to the elapsed time (in seconds) since cart creation beyond which a cart is considered abandoned|

{style="table-layout:auto"}

## Foreign Key Joining Paths

`catalog_product_entity`

*  Join to `catalog_product_entity` table to create columns that return product attributes associated with the cart item.
   *  Path: `quote_item.product_id` (many) => `catalog_product_entity.entity_id` (one)

`quote`

*  Join to `quote` table to create new cart-level columns associated with the cart item.
   *  Path: `quote_item.quote_id` (many) => `quote.entity_id` (one)

`quote_item`

*  Join to `quote_item` to create columns that associate details of the parent configurable or bundle SKU with the simple product. [Contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) for assistance in configuring these calculations, if building in the Data Warehouse manager.
   *  Path: `quote_item.parent_item_id` (many) => `quote_item.item_id` (one)

`store`

*  Join to `store` table to create columns that return details related to the Commerce store associated with the cart item.
   *  Path: `quote_item.store_id` (many) => `store.store_id` (one)
