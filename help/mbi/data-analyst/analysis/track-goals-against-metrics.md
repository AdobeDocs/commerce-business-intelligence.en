---
title: Tracking Goals Against Metrics
description: Learn how to set up a dashboard that will help you track your business goals against your actual data - including revenue, new registered users, and orders over time.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
TQID: https://experienceleague.adobe.com/gT-FJxqVg3X9fuXe-4kWErttYJ6qSMD4eqNvOITNNtQ
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
---
# Tracking Goals Against Performance Metrics

Most clients would like to track their **business goals**, but do not realize this is possible in [!DNL Adobe Commerce Intelligence]. This topic demonstrates how to set up a dashboard that will help you track your business goals against your actual data - including revenue, new registered users, and orders over time. You also learn how to compare year over year performance, all in a dashboard like this:

![Dashboard showing goals tracking against actual metrics performance](../../assets/Goals-_dashboard_2.png)

Before getting started, you should review the [file uploader](../importing-data/connecting-data/using-file-uploader.md) and make sure you have defined your business goals for a given period.

## Getting Started

You need to first upload a file containing specific daily/monthly/quarterly targets for your business.

You can use the [file uploader](../importing-data/connecting-data/using-file-uploader.md) and the image below to format your file. The most common targets that clients track in [!DNL Commerce Intelligence] include Orders, Revenue, and New registered accounts.

![Excel spreadsheet template for tracking goals and metrics](../../assets/Goals-_Excel.png)

## Metrics

Create one new metric for each target. For example, if you upload monthly revenue and orders targets, you need to create two new metrics:

* **Monthly revenue target**
* In the **`Monthly goals`** table
* This metric performs a **Sum**
* On the **`Revenue target`** column
* Ordered by the **`Month`** timestamp

* **Monthly orders target**
* In the **`Monthly goals`** table
* This metric performs a **Sum**
* On the **`Orders target`** column
* Ordered by the **`Month`** timestamp

* **Monthly new registered accounts target**
* In the **`Monthly goals`** table
* This metric performs a **Sum**
* On the **`New registered accounts target`** column
* Ordered by the **`Month`** timestamp

## Reports

It is helpful to have a mix of static values and visual charts when analyzing your targets. Below are three example reports to get you started tracking your revenue performance.

* **Revenue left to achieve target**
* Metric `A`: `Revenue`
* [!UICONTROL Metric]: `Revenue`

* Metric `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* [!UICONTROL Formula]: `(B-A)`
* [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (Whatever relevant time period you want)
* [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Scalar`

* **Revenue targets**
* Metric `A`: `Revenue`
* [!UICONTROL Metric]: `Revenue`

* Metric `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Metric `C`: `Revenue (amount change since previous year)` (hide)
* [!UICONTROL Metric]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (This month last year)
* [!UICONTROL Formula]: `(A-C)`
* [!UICONTROL Format]: `Currency`

* Turn off `Multiple Y-Axes`
* [!UICONTROL Time period]: (Whatever relevant time period you want)*
* [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Once you have completed the above reports for revenue targets, you can create identical reports for goals around orders, registered accounts, or any other values you have included in your goals file upload.

After compiling all the reports, you can organize them on the dashboard as you desire. The result may look like the image at the top of this page.
