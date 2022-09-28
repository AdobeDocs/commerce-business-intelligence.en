---
title: customer_entity table
description: Learn how to access records of all registered accounts.
---
# customer_entity Table

The `customer_entity` table contains records of all registered accounts. An account is considered registered if they sign up for an account, regardless of whether or not they ever complete a purchase. Each row corresponds to one unique registered account, as identified by that account's `entity_id`.

This table does not contain records of customers who place an order via guest checkout. If your store accepts guest checkout, [learn how to account](../data-warehouse-mgr/guest-orders.md) for those customers.

### Common Columns

|**Column Name**|**Description**|
|---|---|
|`created_at`|Timestmap corresponding to the account's registration date, usually stored locally in UTC. Depending on your configuration in MBI, this timestamp may be converted to a reporting time zone in MBI that differs from your database time zone|
|`email`|Email address associated with the account|
|`entity_id` (PK)|Unique identifier for the table, and commonly used in joins to the `customer_id` in other tables within the instance|
|`group_id`|Foreign key associated with the `customer_group` table. Join to `customer_group.customer_group_id` to determine the customer group associated with the registered account|
|`store_id`|Foreign key associated with the `store` table. Join to `store`.`store_id` to determine which Magento store view is associated with the registered account|

### Common Calculated Columns

|**Column Name**|**Description**|
|---|---|
|`Customer's first 30 day revenue`|Sum total of revenue for all orders placed by this customer within 30 days of the customer's first order date. Calculated by joining `customer_entity.entity_id` to `sales_order.customer_id` and summing the `base_grand_total` field for all orders where `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, which is the number of seconds in 30 days|
|`Customer's first order date`|Timestamp of the first order placed by this customer. Calculated by joining `customer_entity.entity_id` to `sales_order.customer_id` and returning the minimum `sales_order`.`created_at` value|
|`Customer's first order's billing region`|Billing region associated with the customer's first order. Calculated by joining `customer_entity.entity_id` to `sales_order.customer_id` and returning the `Billing address region` where `sales_order.Customer's order number` = 1|
|`Customer's first order's coupon_code`|Coupon code associated with the customer's first order. Calculated by joining `customer_entity.entity_id` to `sales_order.customer_id` and returning the `sales_order.coupon_code` where `sales_order.Customer's order number` = 1|
|`Customer's group code`|Group name of the registered customer. Calculated by joining `customer_entity.group_id` to `customer_group`.`customer_group_id` and returning the `customer_group_code` field|
|`Customer's lifetime number of coupons`|Total number of coupons applied to all orders placed by this customer. Calculated by joining `customer_entity.entity_id` to `sales_order.customer_id` and counting the number of orders where the `sales_order.coupon_code` is not `NULL`|
|`Customer's lifetime number of orders`|Total count of orders placed by this customer. Calculated by joining `customer_entity.entity_id` to `sales_order.customer_id` and counting the number of rows in the `sales_order` table|
|`Customer's lifetime revenue`|Sum total of revenue for all orders placed by this customer. Calculated by joining `customer_entity.entity_id` to `sales_order.customer_id` and summing the `base_grand_total` field for all orders placed by this customer|
|`Seconds since customer's first order date`|Elapsed time between the customer's first order date and now. Calculated by subtracting `Customer's first order date` from the server timestamp at the time the query is executed, returned as an integer number of seconds|
|`Store name`|The name of the Magento store associated with this registered account. Calculated by joining `customer_entity.store_id` to `store.store_id` and returning the `name` field|
{:style="table-layout:fixed;"}

### Common Metrics

|**Metric Name**|**Description**|**Construction**|
|---|---|---|
|Avg first 30 day revenue|The average revenue per customer for orders placed within 30 days of the customer's first order|Operation: Average<br/>Operand: `Customer's first 30 day revenue`<br/>Timestamp: `created_at`<br/>Filters:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (excludes customers who have not yet reached 30 days since their first order)|
|Avg lifetime coupons|The average number of coupons applied to orders per customer over their lifetime|Operation: Average<br/>Operand: `Customer's lifetime number of coupons`<br/>Timestamp: `created_at`|
|Avg lifetime orders|The average number of orders placed per customer over their lifetime|Operation: Average<br/>Operand: `Customer's lifetime number of orders`<br/>Timestamp: `created_at`|
|Avg lifetime revenue|The average total revenue per customer for all orders placed over their lifetime|Operation: Average<br/>Operand: `Customer's lifetime revenue`<br/>Timestamp: `created_at`|
|New customers|The number of customers with at least one order, counted on the date of their first order. Excludes accounts who register but never place an order|Operation: Count<br/>Operand: `entity_id`<br/>Timestamp: `Customer's first order date`|
|Registered accounts|The number of accounts registered. Includes all registered accounts, regardless of whether or not the account ever placed an order|Operation: Count<br/>Operand: `entity_id`<br/>Timestamp: `created_at`|
{:style="table-layout:fixed;"}

### Foreign Key Joining Paths

`customer_group`

*  Join to `customer_group` table to create new columns that return the customer group name of the registered account.
   *  Path: `customer_entity.group_id` (many) => `customer_group.customer_group_id` (one)

`store`

*  Join to `store` table to create new columns that return details related to the  store associated with registered account.
   *  Path: `customer_entity.store_id` (many) => `store.store_id` (one)
