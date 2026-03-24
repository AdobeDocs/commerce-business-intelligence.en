---
title: Entity Relationship Diagrams
description: Learn about a few ER diagrams to help you visualize the relationship between a handful of common Commerce database tables.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/pWd5aVoaq2TPkGr37cNeF8CEZ63fItwCEez61eEgGBo
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
# Entity Relationship Diagram

What is an **[!UICONTROL entity relationship (ER) diagram]**? An [!UICONTROL ER] diagram is a visualization of tables within a database and how they relate to each other. This topic contains a few [!UICONTROL ER] diagrams to help you visualize the relationship between a few common Adobe Commerce database tables.

>[!NOTE]
>
>Throughout this topic, you see the words **join**, **relationship**, and **path**. These words are all used to describe how two tables are connected.

## Core Commerce [!UICONTROL ER] Diagram

![4_DB_Chart](../../assets/4_DB_Chart.png)

This `ER` diagram represents the relationships among the core tables within a Commerce database. By viewing multiple relationships at once, you can see how data would relate across many tables.

The sections below contain `ER` diagrams specific to two tables at a time. To view a diagram and its accompanying description, click on the header for that section.

## `customer\_entity & sales\_flat\_order`

![One Customer Many Orders](../../assets/2_OneCustomerManyOrders.png)

One customer can place many orders. The relationship between these two tables is `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` does not equal `sales\_flat\_order.entity\_id`. The first can be thought of as a `customer\_id` and the second can be thought of as an `order\_id.` 

Within [!DNL Commerce Intelligence], if the path between these two tables does not exist, you can [create the path](../data-warehouse-mgr/create-paths-calc-columns.md) within the Data Warehouse tab. When you are ready to create the path, it is defined as follows:

![Entity relationship diagram showing path from sales_flat_order to customer_entity](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

One order can contain many items. The relationship between these two tables is `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Within [!DNL Commerce Intelligence], if the path between these two tables does not exist, you can [create the path](../data-warehouse-mgr/create-paths-calc-columns.md) in the Data Warehouse tab. When you are ready to create the path, define the path as demonstrated below.

![Entity relationship diagram showing path from sales_flat_order_item to sales_flat_order](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

One product can be purchased many items. The relationship between these two tables is `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Within [!DNL Commerce Intelligence], if the path between these two tables does not exist, you can [create the path](../data-warehouse-mgr/create-paths-calc-columns.md) within the Data Warehouse tab. When you are ready to create the path, define the path as demonstrated below.

![Entity relationship diagram showing path from sales_flat_order_item to catalog_product_entity](../../assets/SFOI___CPE_path.png)
