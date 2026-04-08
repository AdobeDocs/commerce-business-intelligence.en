---
title: Expected Commerce Data
description: Explore the main data tables that Commerce users import into Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D-GNfk1-kMscgF1xBKM5xG7wRV4IkIDh9wEBCMGb630
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
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
