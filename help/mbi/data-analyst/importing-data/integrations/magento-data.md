---
title: Expected Magento data
description: Explore the main data tables that Magento users import into MBI
---
# Expected Magento Data

After you have [connected your Magento store](../data-analyst/importing-data/integrations/magento.md), you can use the Data Warehouse Manager to easily track relevant data fields from your Magento database for analysis.

In this article, we explore the main data tables that Magento users import into MBI.

| **Table name** | **Description** |
| Customers | The **customer\_entity** and related tables describe the information associated with each **registered customer** in your database, like their email address and registration date. With this information, you can begin segmenting by customer-level attributes and cohorts. |
| Orders | The **sales\_flat\_order** table records all orders, including the **created\_at** timestamp that the order was placed and the **base\_grand\_total** field that sums up revenue. These fields will be the basis for your order-level metrics. If the order was made by a **registered customer**, the **customer\_id** field will link back to the  **customer\_entity** table to allow analysis on customer buying behavior. |
| Order items | The **sales\_flat\_order\_item** table records each item belonging to an order. This includes the **price** and **qty\_ordered** fields, as well as the **order\_id** field which connects to the **sales\_flat\_order** table. This table is the foundation for metrics like "Item sold", and allows you to segment by **product** and **product type.** |
| Products | The **catalog\_product\_entity** table stores information on product-level attributes, like category, size, and color. |
| Categories | Your products will belong to one or many different **product categories**, depending on how your Magento build is set up. The **catalog\_category\_entity** table stores the hierarchy of these categories (Apprarel -> Tops -> T-Shirts, for example), and the **catalog\_category\_product** table logs the connections between your products and those categories. |

{style="table-layout:auto"}

## Related

* [Connecting Magento](../integrations/magento.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)

