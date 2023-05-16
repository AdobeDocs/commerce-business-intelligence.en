---
title: Expected Commerce Data
description: Explore the main data tables that Commerce users import into Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
---
# Expected [!DNL Adobe Commerce] Data

After you have [connected your [!DNL Adobe Commerce] store](../../../data-analyst/importing-data/integrations/magento.md), you can use the Data Warehouse Manager to easily track relevant data fields from your Commerce database for analysis.

This topic explores the main data tables that Commerce users import into [!DNL Commerce Intelligence].

| **Table name** | **Description** |
|-----|-----|
| `Customers` | The `customer\_entity` and related tables describe the information associated with each *registered customer* in your database, like their email address and registration date. With this information, you can begin segmenting by customer-level attributes and cohorts. |
| `Orders` | The `sales\_flat\_order` table records all orders, including the `created\_at` timestamp that the order was placed and the `base\_grand\_total` field that sums up revenue. These fields are the basis for your order-level metrics. If the order was made by a *registered customer*, the `customer\_id` field links back to the  `customer\_entity` table to allow analysis on customer buying behavior. |
| `Order items` | The `sales\_flat\_order\_item` table records each item belonging to an order. This includes the `price` and `qty\_ordered` fields, and the `order\_id` field which connects to the `sales\_flat\_order` table. This table is the foundation for metrics like `Item sold`, and allows you to segment by `product` and `product type`. |
| `Products` | The `catalog\_product\_entity` table stores information on product-level attributes, like category, size, and color. |
| `Categories` | Your products belong to one or many different `product categories`, depending on how your Commerce build is set up. The `catalog\_category\_entity` table stores the hierarchy of these categories (Apparel > Tops > T-Shirts, for example), and the `catalog\_category\_product` table logs the connections between your products and those categories. |

{style="table-layout:auto"}

## Related

* [Connecting [!DNL Adobe Commerce]](../integrations/magento.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
