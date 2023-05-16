---
title: Build[!DNL Google ECommerce]dimensions
description: Learn to build dimensions that link your eCommerce data with your orders and customer data.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
---
# Build [!DNL Google ECommerce] Dimensions

>[!NOTE]
>
>Requires [Admin permissions](../../administrator/user-management/user-management.md).

Now that you are finished [connecting your[!DNL Google ECommerce] account](../../data-analyst/importing-data/integrations/google-ecommerce.md), what can you do with that data in [!DNL Commerce Intelligence]? This topic walks you through building dimensions that link your eCommerce data with your orders and customer data.

The dimensions covered give you the ability to build analyses that [answer vital questions about your marketing channels and campaigns](../../data-analyst/analysis/most-value-source-channel.md). What percent of revenue comes from each source? How does the lifetime value of [!DNL Facebook] acquired customers compare to those from [!DNL Google]?

## Prerequisites and overview

To create the dimensions in this topic, you need a [!DNL Google ECommerce] table, an `orders` table, and a `customers` table. Those tables must be [synced to your Data Warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) before dimensions can be built. Tables that are synced display in the `Synced Tables` section of the `Data Warehouse Manager`.

Here is a quick look at syncing tables and columns if you need a refresher:

![](../../assets/Syncing_New_Columns.gif)

After creating a join from the `orders` table to the [!DNL Google eCommerce] table, you create the first three dimensions in the list below. Next, you use those dimensions to create three user/customer dimensions in the `customers` table. To finish up, you join those columns to the `orders` table.

Here are the dimensions covered:

* **Orders table**

* Order's [!DNL Google Analytics] source
* Order's [!DNL Google Analytics] medium
* Order's [!DNL Google Analytics]A campaign
* Customer's first order's [!DNL Google Analytics] source
* Customer's first order's [!DNL Google Analytics] medium
* Customer's first order's [!DNL Google Analytics] campaign

* **Customers table**

* Customer's first order's [!DNL Google Analytics] source
* Customer's first order's [!DNL Google Analytics] medium
* Customer's first order's [!DNL Google Analytics] campaign

## Building the dimensions

To create dimensions, open the [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) by clicking **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Orders table, round 1

This example builds the **Order's [!DNL Google Analytics] Source** dimension.

1. From the list of tables in the Data Warehouse, click the table (in this case, `orders`) that contains your order information.
1. Click **[!UICONTROL Create a Column]**.
1. Name the column.
1. Select `Joined Column` from the [definition dropdown](../data-warehouse-mgr/calc-column-types.md). This example works with a [one-to-one relationship](../data-warehouse-mgr/table-relationships.md), matching the `eCommerce.transactionID` column to exactly one row of the `orders` table.
1. Next, you need to define the path, or how the table and column being used are connected. Click the `Select a table and column` dropdown.
1. The path you need is not available, so you need to create a new one. Click **[!UICONTROL Create new Path]**.
1. In the window that displays, set the `Many` side to `orders.order\_id`, or the column in the `orders` table that contains the order ID.
1. On the `One` side, find the `Google ECommerce` table, then set the column to `transactionID`.

    ![](../../assets/google-ecommerce-table.png)

1. Click **[!UICONTROL Save]** to create the path.
1. After the path is added, click the **[!UICONTROL Select table and column]** dropdown again.
1. Locate the `ECommerce` table, and then click the `Source` column. This ties the orders to the source information.
1. Once you are back in the table schema, Click **[!UICONTROL Save]** again to create the dimension.

Here is a look at the whole process:

![](../../assets/help_center.gif)

Next, try creating **Order's [!DNL Google Analytics] medium** and `campaign`. Not much changes for these dimensions, so give it a try. But if you get stuck, you can check out [the end of this article](#stuck) to see what is different.

### Customers table {#customers}

This example builds the **Customer's first order's [!DNL Google Analytics] source** dimension.

1. From the list of tables in the Data Warehouse, click the table (in this case, `customers`) that contains your customer information.
1. Click **[!UICONTROL Create a Column]**.
1. Name the column.
1. For this example, select the `is MAX` definition from the [definition dropdown](../../data-analyst/data-warehouse-mgr/calc-column-types.md). The `is MIN` definition could also work if applied to a text column with only one possible value. The important part is ensuring proper filters are set, which you do later.
1. Click the **[!UICONTROL Select a table and column]** dropdown and select the `orders` table, then the `Order's [!DNL Google Analytics] source` column.
1. Click **[!UICONTROL Save]**.
1. Once you are back in the table schema, click the `Options` dropdown, then `Filters`.
1. Click **[!UICONTROL Add Filter Set]** and then select the `Orders we count` set. You only want orders included in the orders that you count filter set to be included, so it is important that this filter set is selected.
1. Click **[!UICONTROL Add Filter]**. You want to find the customer's first order's [!DNL Google Analytics] source, so you need to add a filter:

    _orders.Customer's order number = 1

    _
1. Click **[!UICONTROL Save]** to create the dimension.

Next, try creating **Customer's first order's [!DNL Google Analytics] medium** and `campaign`. Not much changes for these dimensions, so give it a try. But if you get stuck, you can check out [the end of this article](#stuck) to see what is different.

### Bonus: Orders table, round 2

You can stop here if you want, but this section enables further analysis by bringing the **Customer's first order's [!DNL Google Analytics] dimensions** you created in the [last section](#customers) into the `orders` table. Creating the dimensions in this section lets you analyze all the metrics built on your `orders` table - `Revenue`, `Number of orders`, `Distinct buyers`, and so on - using the [!DNL Google Analytics] attributes of a customer's first order.

This example joins the `Customer's first order's [!DNL Google Analytics] source` dimension to the `orders` table.

1. From the list of tables in the Data Warehouse, click the table (in this case, `orders`) that contains your order information.
1. Click **[!UICONTROL Create a Column]**.
1. Name the column.
1. Select `Joined Column` from the definition dropdown. This joins the customer dimensions that you created in the previous section to the `orders` table.
1. Click the **[!UICONTROL Select a table and column]** dropdown, then select the `customers` table and the `Customer's first order's [!DNL Google Analytics] source` column.
1. If a path does not automatically populate, select the path that best connects the customers and orders tables.
1. Click **[!UICONTROL Save]** to create the dimension.

Here is a look at the whole process:

![](../../assets/help_center2.gif)

Finish up by joining the `Customer's first order's` medium and `campaign` dimensions to the `orders` table. Join the dimensions, and if there are problems, then check out [the end of the article](#stuck) if you need help.

### Wrapping Up

You finished creating the dimensions, which means you can now create powerful analyses that track the performance of your various channels and campaigns. Remember that the **new columns will not be available until after the next update completes**.

 Some of the more popular dimensions are covered in this topic, but the sky is the limit - try creating your own or feel free to ping us if you want help with exploring other options. 

### I am stuck! What is different? {#stuck}

**`Orders` table #1: When creating the `Order's [!DNL Google Analytics]` medium and `campaign` dimensions, the difference is the columns selected in step 12. In this example, the column was `Source`.

**`Customers` table: When creating the `Customer's first order's [!DNL Google Analytics]` medium and `campaign` dimensions, the difference is the columns selected in step 5. In this example, the column was `Order's [!DNL Google Analytics]` source.

**`Orders` table #2: When joining the `Customer's first order's [!DNL Google Analytics]` medium and `campaign` columns to the `orders` table, the difference is the columns selected in step 5. In this example, the column was `Customer's first order's [!DNL Google Analytics]` source.
