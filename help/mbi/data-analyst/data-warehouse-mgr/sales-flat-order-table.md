---
title: sales_order table
description: Learn how to work with the sales_order table.
---
# sales_order Table

The `sales_order` table (`sales_flat_order` on M1) is where each order is captured. In most cases, each row represents one unique order, although there are some custom implementations of Magento that result in splitting an order into separate rows.

This table includes all customer orders, whether or not that order was processed through guest checkout. If your store accepts guest checkout please find more information about this use case [here](https://docs.magento.com/mbi/data-analyst/data-warehouse-mgr/guest-orders.html).

## Common Columns

|**Column Name**|**Description**|
|---|---|
|`base_currency_code`|Currency for all values captured in `base_*` fields (that is `base_grand_total`, `base_subtotal`, and so on). This typically reflects the Magento store's default currency|
|`base_discount_amount`|Discount value applied to order|
|`base_grand_total`|Final price paid by the customer on the order, after all taxes, shipping, and discounts are applied. Although the precise calculation is customizable, in general the `base_grand_total` is calculated as `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount`|
|`base_subtotal`|Gross merchandise value of all items included in the order. Taxes, shipping, discounts and so on are not included|
|`base_shipping_amount`|Shipping value applied to order|
|`base_tax_amount`|Tax value applied to order|
|`billing_address_id`|Foreign key associated with the `sales_order_address` table. Join to `sales_order_address.entity_id` to determine the billing address details associated with the order|
|`coupon_code`|Coupon applied to order. If no coupon is applied, this field will be `NULL`|
|`created_at`|Creation timestamp of the order, usually stored locally in UTC. Depending on your configuration in MBI, this timestamp may be converted to a reporting time zone in MBI that differs from your database time zone|
|`customer_email`|Email address of the customer placing the order. This will be populated in all situations, including orders processed through guest checkout|
|`customer_group_id`|Foreign key associated with the `customer_group` table. Join to `customer_group.customer_group_id` to determine the customer group associated with the order|
|`customer_id`|Foreign key associated with the `customer_entity` table, if the customer is registered. Join to `customer_entity.entity_id` to determine customer attributes associated with the order. If the order was placed through guest checkout, this field will be `NULL`|
|`entity_id` (PK)|Unique identifier for the table, and commonly used in joins to other tables within the Magento instance|
|`increment_id`|Unique identifier for an order, and commonly referred to as the `order_id` within Magento. The `increment_id` is most often used for joins to external sources, such as Google Ecommerce|
|`shipping_address_id`|Foreign key associated with the `sales_order_address` table. Join to `sales_order_address.entity_id` to determine the shipping address details associated with the order|
|`status`|Order's status. May return values such as 'complete', 'processing', 'cancelled', 'refunded', as well as any custom statuses implemented on the Magento instance. Subject to changes as the order gets processed|
|`store_id`|Foreign key associated with the `store` table. Join to `store`.`store_id` to determine which Magento store view is associated with the order|

{style="table-layout:auto"}

## Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|`Billing address city`|Billing city for the order. Calculated by joining `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` and returning the `city` field|
|`Billing address country`|Billing country code for the order. Calculated by joining `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` and returning the `country_id`|
|`Billing address region`|Billing region (most often state or province) for the order. Calculated by joining `sales_order`.`billing_address_id` to `sales_order_address`.`entity_id` and returning the `region` field|
|`Customer's first order date`|Timestamp of the first order placed by this customer. Often considered to be the "acquisition date" for a customer. Calculated by returning the minimum `sales_order`.`created_at` value for each unique customer|
|`Customer's first order's billing region`|Acquisition billing region for the customer who placed the order. Calculated by returning the `Billing address region` associated with the customer's first order|
|`Customer's first order's coupon_code`|Acquisition coupon code for the customer who placed this order. Calculated by returning the `coupon_code` associated with the customer's first order|
|`Customer's group code`|Group name of the customer who placed this order. Calculated by joining `sales_order`.`customer_group_id` to `customer_group`.`customer_group_id` and returning the `customer_group_code` field|
|`Customer's lifetime number of coupons`|Total quantity of coupons applied to all orders placed by this customer. Calculated by counting the number of orders where the `coupon_code` is not `NULL` for each unique customer|
|`Customer's lifetime number of orders`|Total count of orders placed by this customer. Calculated by counting the number of rows in the `sales_order` table for each unique customer|
|`Customer's lifetime revenue`|Sum total of revenue for all orders placed by this customer. Calculated by summing the `base_grand_total` field for all orders for each unique customer|
|`Customer's order number`|Sequential order rank for this customer's order. Calculated by identifying all orders placed by a customer, sorting them in ascending order by the `created_at` timestamp, and assigning an incrementing integer value to each order. For example, the customer's first order returns a `Customer's order number` of 1; their second order returns a `Customer's order number` of 2; and so on|
|`Customer's order number (previous-current)`|Rank of customer's previous order concatenated with the rank of this order, separated by a `-` character. Calculated by concatenating ("`Customer's order number` - 1") with "`-`" followed by "`Customer's order number`". For example, for the order associated with the customer's second purchase, this column will return a value of `1-2`. Most often used when representing the time between two order events (that is, in the "Time between orders" chart)|
|`Is customer's last order?`|Determines whether or not the order corresponds to the customer's last, or most recent, order. Calculated by comparing the `Customer's order number` value with `Customer's lifetime number of orders`. When these two fields are equal for the given order, this column returns "Yes"; otherwise it returns "No"|
|`Number of items in order`|Total quantity of items included in the order. Calculated by joining `sales_order`.`entity_id` to `sales_order_item`.`order_id` and summing the `sales_order_item`.`qty_ordered` field|
|`Seconds between customer's first order date and this order`|Elapsed time between this order and the customer's first order. Calculated by subtracting `Customer's first order date` from the `created_at` for each order, returned as an integer number of seconds|
|`Seconds since previous order`|Elapsed time between this order and the customer's immediately preceding order. Calculated by subtracting the `created_at` for the previous order from the `created_at` of this order, returned as an integer number of seconds. For example, for the order record corresponding to a customer's third order, this column returns the number of seconds between the customer's second order and third order. For the customer's first order, this field will return `NULL`|
|`Shipping address city`|Shipping city for the order. Calculated by joining `sales_order`.`shipping_address_id` to `sales_order_address`.`entity_id` and returning the `city` field|
|`Shipping address country`|Shipping country code for the order. Calculated by joining `sales_order`.`Shipping_address_id` to `sales_order_address`.`entity_id` and returning the `country_id`|
|`Shipping address region`|Shipping region (most often state or province) for the order. Calculated by joining `sales_order`.`shipping_address_id` to `sales_order_address`.`entity_id` and returning the `region` field|
|`Store name`|The name of the Magento store associated with this order. Calculated by joining `sales_order`.`store_id` to `store`.`store_id` and returning the `name` field|

{style="table-layout:auto"}

## Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|Avg order value|The average revenue per order, where revenue is defined as the `base_grand_total`|Operation: Average<br/>Operand: `base_grand_total`<br/>Timestamp: `created_at`|
|Avg time between orders|The average time between a customer's (n-1) order and nth order, for all customers and orders|Operation: Average<br/>Operand: `Seconds since previous order`<br/>Timestamp: `created_at`|
|GMV|The sum of the gross merchandise value for all orders, where GMV is defined as the subtotal, before all taxes and discounts are applied|Operation: Sum<br/>Operand: `base_subtotal`<br/>Timestamp: `created_at`|
|Median time between orders|The median time between a customer's (n-1) order and nth order, for all customers and orders|Operation: Median<br/>Operand: `Seconds since previous order`<br/>Timestamp: `created_at`|
|Orders|The total count of orders placed|Operation: Count<br/>Operand: `entity_id`<br/>Timestamp: `created_at`|
|Revenue|The sum of the revenue for all orders, where revenue is defined as the final price paid by the customer, after all taxes, discounts, shipping, and so on are applied|Operation: Sum<br/>Operand: `base_grand_total`<br/>Timestamp: `created_at`|
|Shipping|The sum of the shipping amount for all orders|Operation: Sum<br/>Operand: `base_shipping_amount`<br/>Timestamp: `created_at`|
|Tax|The sum of the taxes applied to all orders|Operation: Sum<br/>Operand: `base_tax_amount`<br/>Timestamp: `created_at`|
|Unique Customers|The number of unique customers placing an order in the given reporting time interval. For example if the report's interval was weekly, each customer who places at least one order in a given week will be counted exactly once, regardless of how many orders they placed in that week|Operation: Count Distinct<br/>Operand: `customer_email`<br/>Timestamp: `created_at`|

{style="table-layout:auto"}

## Foreign Key Joining Paths

`customer_entity`

*  Join to `customer_entity` table to create new customer-level columns associated with the customer who placed the order.
   *  Path: `sales_order.customer_id` (many) => `customer_entity.entity_id` (one)

`customer_group`

*  Join to `customer_group` table to create new columns that return the customer group name of the customer who placed the order.
   *  Path: `sales_order.customer_group_id` (many) => `customer_group.customer_group_id` (one)

`sales_order_address`

*  Join to `sales_order_address` table to create new columns that return billing and shipping locations associatd with the order. Two joining paths are possible, depending on whether the billing or shipping details are required.
   *  Paths:
      *  Shipping: `sales_order.shipping_address_id`(many) => `sales_order_address.entity_id` (one)
      *  Billing: `sales_order.billing_address_id`(many) => `sales_order_address.entity_id` (one)

`store`

*  Join to `store` table to create new columns that return details related to the Magento store associated with the order.
   *  Path: `sales_order.store_id` (many) => `store.store_id` (one) 
