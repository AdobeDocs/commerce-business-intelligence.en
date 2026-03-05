---
title: Reduce Your Update Cycle Time
description: Learn how to reduce your update cycle time.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/DFlzL9E95teiWI31j7qWRU8Ab6GkbFX7iPPdaxGq48A
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
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Reduce Update Cycle Processing Time

[!DNL Adobe Commerce Intelligence] syncs with your database throughout the day to replicate new data, ensuring that your dashboards always show the latest information.

Many factors can add to an already lengthy update time. Certain replication methods, higher recheck frequencies, and the number of dashboards and charts are just a few contributors. This topics discusses some best practices to reduce your update times.

## Decrease Recheck Frequency

In a database table, there can be data columns with changeable values. For example, in an **orders** table there might be a column called **status**. When an order is initially written to the database, the status column might contain the value `pending`. The order is replicated in your [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) with this `pending` value.

Changeable columns must be [rechecked for updated values](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) over time. By default, [!DNL Commerce Intelligence] rechecks these columns during every update, but if there is a large amount of data to be rechecked and replicated, it can negatively impact your update time. Instead of running rechecks during every update, Adobe recommends setting the recheck frequency to daily, weekly, or monthly.

## Use Incremental Replication Methods

As mentioned above, long update times are directly correlated to how much data has to be rechecked and replicated. [Incremental replication methods](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) can greatly reduce the amount of data processed during the update cycle. Where possible, Adobe recommends using these methods or modifying your database to support an incremental method.

## Remove Unused Charts from Dashboards

At the end of the update cycle, [!DNL Commerce Intelligence] performs a cache operation for all charts. A cache stores data so future requests for information can be completed faster. In [!DNL Commerce Intelligence], this means dashboards load quickly because charts do not need to query data every time they load.

Since [!DNL Commerce Intelligence] only performs cache operations for charts found in a dashboard, removing unused charts from your dashboards decreases your update time. Keep in mind that the same chart might be on multiple dashboards - check with your team to make sure they also removed any unused charts.

>[!NOTE]
>
>Removing charts from your dashboard does not delete the chart. You can [add it back anytime](../data-user/dashboards/add-charts-dashboard.md).

## Optimize Your Database for Analysis

In addition to reevaluating recheck frequencies, replication methods, and chart usefulness, you can also [optimize your database for analysis](../best-practices/opt-db-analysis.md).

## Wrapping Up

If your update time still seems slow even after implementing these recommendations, [contact the support team](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
