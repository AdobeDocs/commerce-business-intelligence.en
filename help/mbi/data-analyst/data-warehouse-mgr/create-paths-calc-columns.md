---
title: Create or delete paths for calculated columns
description: Learn how to define a path describing how the table you are creating a column on is related to the table you are pulling information from.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
---
# Create or Delete Paths for Calculated Columns

## Calculated Columns Refresher

When [creating calculated columns](../data-warehouse-mgr/creating-calculated-columns.md) in your Data Warehouse, you are asked to define a path describing how the table you are creating a column on is related to the table you are pulling information from. To successfully create a path, you need to know two things:

1. How the tables in your databases relate to each other
1. The primary and foreign keys that define this relationship

If you know this information, you are able to easily create a path following the instructions in this article. An overview of these concepts if you are feeling a little unsure, but you may want to ask a technical expert in your organization or contact the Adobe support team.

## Refreshers on table relationships and key types {#refresher}

### Table Relationships {#relationships}

This concept is covered in the [Understanding and evaluating table relationships article](../../data-analyst/data-warehouse-mgr/table-relationships.md), but a quick summary never hurt anyone, right?

Tables can be related to one another in one of three ways:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | The relationship between people and driver's license numbers. A person can have only one driver's license number, and a driver's license number belongs to only one person. |
| **`one-to-many`** | The relationship between orders and items - an order can contain many items, but an item belongs to a single order. In this case, the orders table is the one side and the items table is the many side. |
| **`many-to-many`** | The relationship between products and categories: a product can belong to many categories, and a category can contain many products. |

{style="table-layout:auto"}

Once a relationship between two tables is understood, it can be used to determine what path should be created to bring information from one table to another. This next step requires knowing the primary and foreign keys that facilitate a table relationship.

### Primary and foreign keys {#keys}

A `Primary Key` is an unchanging column or set of columns that produces unique values within a table. For example, when a customer makes an order on a website, a new row is added to the `orders` table in your shopping cart, with a new `order_id`. This `order_id` allows both the customer and business to track the progress of that specific order. Because order id is unique, it is typically the `Primary Key` of an `orders` table.

A `Foreign Key` is a column created inside a table that links to the `Primary Key` column of another table. Foreign Keys create references between tables, allowing analysts to easily look up and link records together. Say you wanted to know which orders belonged to each of your customers. The `customer id` column (`Primary Key` of the `customers` table) and the `order_id` column (`Foreign Key` in the `customers` table, referencing the `Primary Key` of the `orders` table) allows us to link and analyze this information. When creating a path, you are asked to define both the `Primary Key` and `Foreign Key`.

## Creating a Path {#createpath}

When creating a column in your Data Warehouse, you must define the path that brings information from one table into another. Sometimes paths pre-populate because a path exists between tables, but if this does not happen, you must create one.

Use the relationship between **customers** and **orders** to show you how it is done. Broken down:

* The relationship is `one-to-many` - a customer can have many orders, but an order can have only one customer. This tells us the direction of the relationship, or where the calculated column should be created. In this case, it means information from the `orders` table can be brought into the `customers` table.
* The `primary key` you want to use is `customers.customerid`, or the `customer ID` column in the `customers` table.
* The `foreign key` you want to use is `orders.customerid`, or the `customer ID` column in the `orders` table.

Now, you can create the path.

1. Click **[!UICONTROL Data > Data Warehouse]**.
1. In the table list, click the table you want to create the column in. In this example, it is the `customers` table.
1. The table schema displays. Click **[!UICONTROL Create New Column]**.
1. Give your column a name - for example, `Customer's orders`.
1. Select the definition for the column. Check out the [Calculated Column Guide](../data-warehouse-mgr/creating-calculated-columns.md) for a handy cheat sheet.
1. In the [!UICONTROL Select table and column] dropdown, click the **[!UICONTROL Create new path]** option. 

    ![Creating paths for calculated columns modal](../../assets/Creating_Paths_modal.png)

1. Using the dropdowns, select the primary and foreign keys for each table.

     On the `Many` side, you select `orders.customerid` - remember, customers can have many orders.

     On the `One` side, you select `customers.customerid` - an order can only have one customer.

1. Click **[!UICONTROL Save]** to save the path and finish creating the column.

### Limitations of Creating Paths {#limits}

* **[!DNL Commerce Intelligence] cannot guess primary/foreign key relationships**. You do not want to introduce incorrect data into your account, so creating paths must be done manually.
* **Currently, paths can only be specified between two different tables**. Does the logic that you are trying to recreate involve more than two tables? It then might make sense to (1) join the columns to an intermediary table first, then to the "final destination" table, or (2) consult with the Adobe team to find the best approach to your goals.
* **A column can only be the foreign key reference for ONE path at one time**. For example, if `order_items.order_id` points to `orders.id`, then `order_items.order_id` cannot point to anything else.
* **`Many-to-many` paths can technically be created, but often produce bad data because neither side is a true `one-to-many` foreign key**. The best way to approach these paths always depend on the specific desired analysis. Consult the RJ analyst team to uncovering the best solution.

If you are prevented from creating a calculated column due to one or more of the limitations above, contact support with a description of the column you are

## Delete a Calculated Column Path {#delete}

Created an incorrect path in your Data Warehouse? Or maybe you are doing a little spring cleaning and want to tidy up? If you need to delete a path from your account, you can [send a ticket over to Adobe support analysts](../../guide-overview.md). **Be sure to include the name of the path!**

## Wrapping up {#wrapup}

Now that you are comfortable creating paths for calculated columns in your Data Warehouse. If you are still unsure about a particular path, remember that you can always click **[!UICONTROL Support]** in your [!DNL Commerce Intelligence] account to get assistance.

## Related

* [Understanding and evaluating table relationships](../data-warehouse-mgr/table-relationships.md)
* [Creating paths for calculated columns](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Calculated Column Types](../data-warehouse-mgr/calc-column-types.md) attempting to create.
