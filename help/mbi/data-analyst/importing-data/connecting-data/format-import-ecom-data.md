---
title: Formatting and importing eCommerce data
description: Learn the ideal data formats to be used for uploading eCommerce data.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
---
# Formatting and Importing Data

If you are using an integration not currently supported by [!DNL Commerce Intelligence], you can still use the [File Upload feature](using-file-uploader.md) to get your data into your Data Warehouse. This topic covers the ideal data formats to be used for uploading eCommerce data.

## `Orders` table

The `orders` table should contain one row for every transaction the business has conducted. Potential columns include:

| Column name | Description |
|----|----|
| `Order ID` | The order ID should be unique for every row in the table. Also, this is typically the primary key for the table. |
| `Customer` | The customer who placed the order. |
| `Order total` | The total of the order. This may be a calculation-based column, where values in other columns - such as subtotal and shipping - make up the total for this column. |
| `Currency` | The currency the order was paid in. Include if relevant. |
|` Order status` | The status of the order, such as `In Progress`, `Refunded`, or `Complete`. The value of this column changes (if not complete). New and updated data can be imported using the [Append Data feature](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) on the `File Uploads` page. |
| `Acquisition/marketing channel` | The acquisition or marketing channel that the customer who placed the order was referred from. |
| `Order datetime` | The date and time the order was created. |
| `Order updated at` | The date and time the last modification to the order record was made. |

{style="table-layout:auto"}

## `Order detail/items` table {#itemstable}

The `order_detail / items` table should contain one row for each distinct item in every order. Potential columns include:

| Column name| Description |
|----|----|
| `Order item ID` | The order item ID should be unique for every row in the table. Also, this is typically the `primary key` for the table. |
| `Order ID` | The ID of the order. |
| `Product ID` | The product's ID. |
| `Product name` | The name of the product. |
| `Product's unit price` | The price for a single unit of the product. |
| `Quantity` | The quantity of the product in the order. |

## `Customers` table {#customerstable}

The `customers` table should contain one row for each customer account. Potential columns include:

| Column name| Description |
|----|----|
| `Customer ID` | The customer ID should be unique for every row in the table. Also, this is typically the primary key for the table. |
| `Customer created at` | The date and time the customer's account was created. |
| `Customer modified at` | The date and time the customer's account was last modified. |
| `Acquisition/marketing channel source` | The acquisition or marketing channel that the customer was referred from. |
| `Demographic info` | Demographic info such as age range and gender can be used to segment your reports.  |
| `Acquisition/marketing channel` | The acquisition or marketing channel that the customer who placed the order was referred from. |

## `Subscription payments` table

The `subscriptions` table should contain one row for each subscription payment. Potential columns include:

| Column name| Description |
|----|----|
| `Subscription ID` | The subscription ID should be unique for every row in the table. Also, this is typically the primary key for the table. |
| `Customer ID` | The ID of the customer who made the payment. |
| `Payment amount` | The amount of the subscription payment. |
| `Start date` | The starting datetime of the period that the payment covers. |
| `End date` | The ending datetime of the period that the payment covers. |
