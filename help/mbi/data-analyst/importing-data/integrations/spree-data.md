---
title: Expected Spree data
description: Explore the main data tables that you can import from Spree into your MBI account.
---
# Expected Spree data

After you have [connected your Spree store](../data-analyst/importing-data/integrations/spree.md), you can use the [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields from your Spree platform for analysis.

In this article, we explore the main data tables that you can import from Spree into your MBI account, including links to [additional documentation](https://guides.spreecommerce.org/developer/addresses.html#address) about Spree data.

| **Table name** | **Description** |
| Users | The **users** table includes the account details for registered customers, including the individual's email, name, and registration date. This allows you to analyze different customer segments and their buying behaviors. |
| [Orders](https://guides.spreecommerce.org/developer/orders.html#overview) | The **orders** table serves as the foundation for all of your order-level metrics. Recorded here are all order details of purchases from your Spree store, including completed\_at (the timestamp of the order), user\_id (id of registered user who placed the order). If the order was made by a registered user, the user\_id will link back to the **users** table to allow analysis on user buying behavior. |
| Line items | The **line\_items** table is a child of either the **orders** table or **subscriptions**. It records an order's or a subscription's line item details. For orders with multiple products, each product will have its own data row in this table, including a product\_id that allows you to tie it to the **products** table. |
| [Products](https://guides.spreecommerce.com/developer/products.html#overview) | The **products** table records all product details for a saleable item in your Spree catalog. This allows you to segment your line item-level metrics by product attributes. |
| Subscriptions | If you have a Spree subscriptions extension, the **subscriptions** table holds each individual subscription's information, including created\_at (the start date), cancelled\_at (the date a subscription was cancelled), and the interval of the subscription. |
{style="table-layout:auto"}

## Related:

* [Connecting Spree](../integrations/spree.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
