---
title: Tracking Goals Against Metrics
description: Learn how to set up a dashboard that will help you track your business goals against your actual data - including revenue, new registered users, and orders over time.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
---
# Tracking Goals Against Performance Metrics

A large majority of our clients often would like to track their **business goals**, but do not realize this is possible in [!DNL MBI]. In this article, we demonstrate how to set up a dashboard that will help you track your business goals against your actual data - including revenue, new registered users, and orders over time. We also show you how to compare year over year performance, all in a dashboard like this:

![](../../assets/Goals-_dashboard_2.png)

Before getting started, you want to familiarize yourself with our [file uploader](../importing-data/connecting-data/using-file-uploader.md) and make sure you have defined your business goals for a given period of time.

## Getting Started

You will need to first upload a file containing specific daily/monthly/quarterly targets for your business.

You can use the [file uploader](../importing-data/connecting-data/using-file-uploader.md) and the image below to format your file. The most common targets that our clients track in [!DNL MBI] include Orders, Revenue, and New registered accounts.

![](../../assets/Goals-_Excel.png)

## Metrics

You need to create one new metric for each target. For example, if you upload monthly revenue and orders targets, you will need to create two new metrics:

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

As always, it is helpful to have a mix of static values and visual charts when analyzing your targets. Below are three example reports to get you started tracking your revenue performance.

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

After compiling all the reports, you can organize them on the dashboard as you desire. The end result may look like the image at the top of this page.
