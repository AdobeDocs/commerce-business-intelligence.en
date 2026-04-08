---
title: Expected Spree data
description: Explore the main data tables that you can import from Spree into your [!DNL Commerce Intelligence] account.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/DhJhNDqTEki-evyidC-9d08qq-XSDPRu1jJqG1lOijI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Expected [!DNL Spree] data

After you have [connected your [!DNL Spree] store](../../../data-analyst/importing-data/integrations/spree.md), you can use the [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields from your [!DNL Spree] platform for analysis.

This topic explores the main data tables that you can import from [!DNL Spree] into your [!DNL Commerce Intelligence] account, including links to [additional documentation](https://guides.spreecommerce.org/developer/addresses.html#address) about [!DNL Spree] data.

| **Table name** | **Description** |
|-----|-----|
| `Users` | The `users` table includes the account details for registered customers, including the individual's email, name, and registration date. This allows you to analyze different customer segments and their buying behaviors. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | The `orders` table serves as the foundation for all of your order-level metrics. Recorded here are all order details of purchases from your [!DNL Spree] store, including `completed\_at` (the timestamp of the order), `user\_id` (id of registered user who placed the order). If the order was made by a registered user, the `user\_id` links back to the `users` table to allow analysis on user buying behavior. |
| `Line items` | The `line\_items` table is a child of either the `orders` table or `subscriptions`. It records an order's or a subscription's line item details. For orders with multiple products, each product has its own data row in this table, including a `product\_id` that allows you to tie it to the `Products` table. |
| `Products` | The `products` table records all product details for a saleable item in your Spree catalog. This allows you to segment your line item-level metrics by product attributes. |
| `Subscriptions` | If you have a [!DNL Spree] subscriptions extension, the `subscriptions` table holds each individual subscription's information, including `created\_at` (the start date), `cancelled\_at` (the date a subscription was cancelled), and the `interval` of the subscription. |

{style="table-layout:auto"}

## Related:

* [Connecting [!DNL Spree]](../integrations/spree.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
