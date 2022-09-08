---
title: Common Magento Tables
zendesk_id: 360016504772
---

When you first [connect a Magento instance to MBI](../importing-data/integrations/magento.md), MBI automatically replicates data from some of your commerce tables (typically 4-6 tables) in order to configure the initial set of dashboards and reports. Although this offers a great starting point, most store instances generate tens if not hundreds of additional tables which can provide critical insight into the performance of your business.

Below is a list of some of the more common tables that MBI customers utilize. After you [connect your Magento instance to MBI](../data-analyst/importing-data/integrations/magento.md), you can use the [Data Warehouse Manager](../data-analyst/data-warehouse-mgr/tour-dwm.md %}#calculated) to track relevant data fields.

|Table name|Description|
|---|---|
|`catalog_category_entity`|Each row in the `catalog_category_entity` table describes a specific category. With the associated `catalog_category_entity_varchar` table and the `catalog_category_product` mapping table, you can obtain category information for each product.|
|`catalog_category_product`|Each row in the `catalog_category_product` table lists a combination of a product and a category. Therefore, a given product can exist on this table multiple times with different categories, and a given category can exist on this table multiple times associated with different products. This table indexes the `catalog_category_entity` table (which holds category-level details) and the `catalog_product_entity` table (which holds product-level details).|
|`catalog_product_entity`|Each row in the `catalog_product_entity` table represents a specific product. This includes when that product was created in your Magento account and its SKU.|
|`customer_entity`|Each row in the [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) table represents a registered user on your website. Basic customer-level details like their registration date and email address live on this table.|
|`quote`|Each row in the [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) table represents a cart that was created in the checkout process, whether or not that cart eventually converted to an order. Due to the potential size of this table, we recommend you periodically delete records if certain criteria are met, such as if there are any unconverted carts older than 60 days.|
|`quote_item`|Each row in the [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) table represents an item added to a cart, whether or not the cart eventually converted to an order. Due to the potential size of this table, we recommend you periodically delete records if certain criteria are met, such as if there are any unconverted carts older than 60 days.|
|`sales_order`|Each row in the [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) table represents an order placed on your site. This table contains order-level information such as the order's date, the customer who placed the order, the order total, and discount and coupon code usage.|
|`sales_order_address`|Each row on the `sales_order_address` table contains shipping and billing information for a specific order. On the `sales_order` table, the `billing_address_id` and the `shipping_address_id` for a given order refer to a specific row (identified by `entity_id`) on the `sales_order_address` table.|
|`sales_order_item`|Each row in the [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) table identifies a specific item from a specific order. Each row contains details such as the product, the quantity purchased, and the order with which the given item is associated.|

### Related documentation

[Magento Entity Relationship Diagrams](../data-warehouse-mgr/entity-rel-diag.md)
