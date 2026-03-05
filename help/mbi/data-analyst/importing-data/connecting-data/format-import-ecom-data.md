---
title: Formatting and importing eCommerce data
description: Learn the ideal data formats to be used for uploading eCommerce data.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/3Aa9DgQL0H9cNeJOJ7-qHkROOkphjzpQkDvJ0KwOIwY
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
# Formatting and Importing Data

If you are using an integration not currently supported by [!DNL Adobe Commerce Intelligence], you can still use the [File Upload feature](using-file-uploader.md) to get your data into your Data Warehouse. This topic covers the ideal data formats to be used for uploading ecommerce data.

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
