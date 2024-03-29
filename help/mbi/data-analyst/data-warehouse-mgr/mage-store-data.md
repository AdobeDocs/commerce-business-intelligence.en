---
title: Storing Data in Adobe Commerce
description: Learn how data is generated, what causes a new row to be inserted , and how actions are recorded into the Adobe Commerce database.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
---
# Storing Data in [!DNL Adobe Commerce]

The [!DNL Adobe Commerce] platform records and organizes a wide variety of valuable commerce data across hundreds of tables. This topic describes:

* how that data is generated
* what causes a new row to be inserted into one of the [Core Commerce Tables](../data-warehouse-mgr/common-mage-tables.md)
* how actions such as making a purchase or creating an account are recorded into the [!DNL Adobe Commerce] database

To discuss these concepts, refer to the following example:

`Clothes4U` is a clothing retailer with both an online and brick and mortar presences. It uses [!DNL Magento Open Source] behind its website to gather and organize data.

## `catalog\_product\_entity`

It is September 22, and `Clothes4U` is rolling out three new items to its Fall line: `Throwback Bellbottoms`, `Straight Leg Jeans`, and `V-Neck T-Shirts`. A `Clothes4U` employee opens their Commerce Admin, clicks **[!UICONTROL Add Product]**, and enters all the information for `Throwback Bellbottoms`.

Satisfied with all the settings for `Throwback Bellbottoms`, the employee clicks **[!UICONTROL Save]**, which inserts the first line below into the `catalog_product_entity` table. The employee repeats the process, creating another Commerce product for `Straight Leg Jeans`, and then a third for `V-Neck T-Shirt`, inserting the second and third lines below into the `catalog_product_entity` table:

|**`entity\_id`**|**`entity\_type\_id`**|**`attribute\_set\_id`**|**`sku`**|**`created\_at`**|
|---|---|---|---|---|
|205|4|8|Pants10|2016/09/22 09:15:43|
|206|4|8|Pants11|2016/09/22 09:18:17|
|207|4|12|Shirts6|2016/09/22 09:24:02|

* `entity_id` – This is the primary key of the `catalog_product_entity` table, meaning every row of the table must have a different `entity_id`. Each `entity_id` on this table can only be associated with one product, and each product can only be associated with one `entity_id`
    * The top line of the table above, `entity_id` = 205, is the new row created for "Throwback Bellbottoms." Wherever `entity_id` = 205 appears in the Commerce platform, it is referring to the product "Throwback Bellbottoms"
* `entity_type_id` – Commerce has multiple categories of objects (like customers, addresses, and products to name a few), and this column is used to denote the category into which this particular row falls.
    * This being the `catalog_product_entity` table, each row has the same entity type: product. In Adobe Commerce, the `entity_type_id` for product is 4, which is why all three of the new products created return 4 for this column.
* `attribute_set_id` – Attribute sets are used to identify products that have the same of descriptors.
    * The top two rows of the table are the `Throwback Bellbottoms` and `Straight Leg Jeans` products, both of which are pants. These products would have the same descriptors (for example, name, inseam, waistline), and therefore have the same `attribute_set_id`. The third item, `V-Neck T-Shirt` has a different `attribute_set_id` because it would not have the same descriptors as the pants; shirts do not have waistlines or inseams.
* `sku` - These are unique values assigned to each product by the user when creating a product in Adobe Commerce.
* `created_at` - This column returns the timestamp of when each product was created

## `customer\_entity`

Shortly after the addition of the three new products, a new customer, `Sammy Customer`, visits `Clothes4U`'s website for the first time. Since `Clothes4U` does not allow guest orders, `Sammy Customer` must first create an account on the website. Customer enters required credentials and clicks submit, resulting in the following new entry on the [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

|**`entity id`**|**`entity type id`**|**`email`**|**`created at`**|
|---|---|---|---|
|`214`|`1`|`sammy.customer@gmail.com`|`2016/09/23 15:27:12`|

* `entity_id` - Just like the prior table, `entity_id` is the primary key of the `customer_entity` table.
    * When `Sammy Customer` created an account and the row above was written to the `customer_entity` table, customer was assigned `entity_id` = 214. Throughout all tables, the customer identified as `entity_id` = 214 always refers to the user Sammy Customer
* `entity_type_id` – This column identifies which type of entity is being listed in this table, and functions the same way as it does in the `catalog_product_entity` table
    * Every row on the `customer_entity` table is a customer, and Commerce defines customers as `entity_type_id` 1 by default
* `email` – this field is populated by the email that a new customer enters when making their account
* `created_at` – This column returns the timestamp for when each user joined

## `sales\_flat\_order (or Sales\_order` if you have [!DNL Adobe Commerce 2.x]

With the account creation finished, `Sammy Customer` is ready to start making a purchase. On the website, the customer adds two pairs of the `Throwback Bellbottoms` and one `V-Neck T-Shirt` to the cart. Satisfied with the selections, the customer moves to checkout and submits the order, creating the following entry on the [sales flat order table](../data-warehouse-mgr/sales-flat-order-table.md):

|**`entity id`**|**`customer id**`|**`subtotal`**|**`created at`**|
|---|---|---|---|
|227|214|94.85|2016/09/23 15:41:39|

* `entity_id` – this is the primary key of the `sales_flat_order` table.
    * When Sammy Customer placed this order and the row above was written to the `sales_flat_order` table, the order was assigned `entity_id` = 227.
* `customer_id` – This column is the unique identifier of the customer who placed this particular order
    * The `customer_id` associated with this order is 214, which is Sammy Customer's `entity_id` on the `customer_entity` table.
* `subtotal` – This column is the total amount charged to a customer for the order
    * The two pairs of "Throwback Bellbottoms" and the "V-Neck T-Shirt" cost $94.85 dollars in total
* `created_at` – This column returns the timestamp for when each order was created

## `sales\_flat\_order\_item ( or Sales\_order\_item` 

(if you have Commerce 2.0 or later)

In addition to the single row on the `Sales\_flat\_order` table, when `Sammy Customer` submits the order, a row for each unique item in that order is inserted into the [`sales\_flat\_order\_item` table](../data-warehouse-mgr/sales-flat-order-item-table.md):

|**`item\_id`**|**`name`**|**`product\_id`**|**`order\_id`**|**`qty\_ordered`**|**`price`**|
|---|---|---|---|---|---|
|822|`Throwback Bellbottoms`|205|227|2|39.95|
|823|`V-Neck T-Shirt`|207|227|1|14.95|

* `item_id` – This column is the primary key of the `sales_flat_order_item` table
    * `Sammy Customer`'s order has created two lines on this table because the order contained two distinct products
* `name` – This column is the name of the product
* `product_id` – This column is the unique identifier of the product to which this row is referring
    * The first row above has `product_id` = 205 because `Throwback Bellbottoms` have an `entity_id` of 205 on the `catalog_product_entity` table
* `order_id` - This column is the `entity_id` of the order that contains these particular order items
    * Both rows above have `order_id` = 227 because they are both part of the order placed by `Sammy Customer`, which has `entity_id` = 227 on the `sales_flat_order` table
* `qty_ordered` – This column is the number of units of the product that are included in this specific order
    * `Sammy Customer`'s order contained two pairs of `Throwback Bellbottoms`
* `price` – This column is the price of a single unit of the order item
    * The `subtotal` from `Sammy Customer`'s order in the `sales_flat_order` table was 94.85, which is the sum of two pairs of `Throwback Bellbottoms` at $39.95 each and 1 `V-Neck T-Shirt` at $14.95.
