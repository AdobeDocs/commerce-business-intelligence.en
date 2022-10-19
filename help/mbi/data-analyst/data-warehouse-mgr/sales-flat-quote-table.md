---
title: quote table
description: Learn how to work with the quote table.
---
# quote Table

The `quote` table (`sales_flat_quote` on M1) contains records on every shopping cart created in your store, whether they were abandoned or converted to a purchase. Each row represents one cart. Due to the potential size of this table, we recommend you periodically delete records if certain criteria are met, such as if there are any unconverted carts older than 60 days.

>[!NOTE]
>
>Analyzing historical abandoned carts is only possible if you do not delete records from the `quote` table. If you do delete records, you will only be able to see the carts not yet removed from your database.

## Common Native Columns

|**Column Name**|**Description**|
|---|---|
|`base_currency_code`|Currency for all values captured in `base_*` fields (that is `base_grand_total`, `base_subtotal`, and so on). This typically reflects the Magento store's default currency|
|`base_grand_total`|Final price quoted to the customer for the cart, after all taxes, shipping, and discounts are applied. Although the precise calculation is customizable, in general the `base_grand_total` is calculated as `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount`|
|`base_subtotal`|Gross merchandise value of all items included in the cart. Taxes, shipping, discounts and so on are not included|
|`created_at`|Creation timestamp of the cart, usually stored locally in UTC. Depending on your configuration in MBI, this timestamp may be converted to a reporting time zone in [!DNL MBI] that differs from your database time zone|
|`customer_email`|Email address of the customer who created the cart|
|`customer_id`|Foreign key associated with the `customer_entity` table, if the customer is registered. Join to `customer_entity.entity_id` to determine customer attributes associated with the user who created the cart. If the cart was created through guest checkout, this field will be `NULL`|
|`entity_id` (PK)|Unique identifier for the table, and commonly used in joins to other tables within the Magento instance|
|`is_active`|Boolean field that returns "1" if the cart was created by a customer and has not yet converted to an order. Returns "0" for converted carts, or carts created through the admin|
|`items_qty`|Sum of the total quantity of all items included in the cart|
|`reserved_order_id`|Foreign key associated with the `sales_order` table. Join to `sales_order.increment_id` to determine order details associated with a converted cart. For carts that are not associated with a converted order, the `reserved_order_id` will remain `NULL`|
|`store_id`|Foreign key associated with the `store` table. Join to `store`.`store_id` to determine which Magento store view is associated with the cart|

{style="table-layout:auto"}

## Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|`Order date`|Timestamp reflecting order creation date for converted carts. Calculated by joining `quote.reserved_order_id` to `sales_order.increment_id` and returning the `sales_order.created_at` field |
|`Seconds between cart creation and order`|Elapsed time between cart creation and order creation. Calculated by subtracting `created_at` from `Order date`, returned as an integer number of seconds|
|`Seconds since cart creation`|Elapsed time between the cart's creation date and now. Calculated by subtracting `created_at` from the server timestamp at the time the query is executed, returned as an integer number of seconds. Most commonly used to identify the age of a cart|
|`Store name`|The name of the Magento store associated with this order. Calculated by joining `quote.store_id` to `store.store_id` and returning the `name` field|

{style="table-layout:auto"}

## Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|Number of abandoned carts|The count of carts that meet specific "abandonment" conditions|Operation: Count<br/>Operand: `entity_id`<br/>Timestamp: `created_at`<br/>Filters:<br><br>- \[A\] `is_active` = 1<br>- \[B\] `items_count` > 0<br>- \[C\] `Seconds since cart creation` > x, where "x" corresponds to the elapsed time (in seconds) since cart creation beyond which a cart is considered abandoned|
|Avg time to cart conversion|The average time between cart creation and order creation for converted carts|Operation: Average<br>Operand: `Seconds between cart creation and order`<br>Timestamp: `created_at`|
|Abandoned cart value|The sum of the total abandoned cart potential revenue, where revenue is defined as the `base_grand_total` field|Operation: Sum<br>Operand: `base_grand_total`<br>Timestamp: `created_at`<br>Filters:<br><br>- \[A\] `is_active` = 1<br>- \[B\] `items_count` > 0<br>- \[C\] `Seconds since cart creation` > x, where "x" corresponds to the elapsed time (in seconds) since cart creation beyond which a cart is considered abandoned|

{style="table-layout:auto"}

## Foreign Key Joining Paths

`customer_entity`

*  Join to `customer_entity` table to create new customer-level columns associated with the customer who created the cart.
   *  Path: `quote.customer_id` (many) => `customer_entity.entity_id` (one)

`sales_order`

*  Join to `sales_order` table to create new columns that return order details associated with a converted cart.
   *  Path:`quote.reserved_order_id` (many) => `sales_order.increment_id` (one)

`store`

*  Join to `store` table to create new columns that return details related to the Magento store associated with the cart.
   *  Path: `quote.store_id` (many) => `store.store_id` (one)
