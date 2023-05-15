---
title: Data and Updates Information
description: Learn how to check the status of your update cycle.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
---
# Data and Updates Information

* [Why did my data change?](#datachange)
* [What is the difference between a regular and forced update?](#regularforcedupdates)
* [Why does the update cycle take a long time?](#updatecycletime)
* [Can I be notified when an update cycle completes?](#notifyupdate)
* [Why is [!DNL Google ECommerce] data different from my database?](#ecommdatabase)
* [How do I troubleshoot a data discrepancy?](#datadiscrepancy)

## Why did my data change? {#datachange}

Chart values can change throughout the day due to new data being synced to your Data Warehouse. Also, values for existing data columns can change due to [rechecks](../data-warehouse-mgr/cfg-data-rechecks.md). A recheck is a process that looks for changed values in data columns - for example, an order status moving from `open` to `shipped`.

There are a few different ways [to check the status of your update cycle](../../best-practices/check-update-cycle.md), depending on the type of user permissions you have.

## What is the difference between a regular and forced update? {#regularforcedupdates}

Regular updates are **scheduled** processes while forced updates are **manual processes initiated by you**. If you have blackout hours - or a time period where [!DNL Commerce Intelligence] should not update your data - forcing an update starts a cycle that does not respect the limitations of the blackout period.

## Why does the update cycle take a long time? {#updatecycletime}

Numerous factors can add to an already lengthy update time. Certain [replication methods](../data-warehouse-mgr/cfg-replication-methods.md), [higher recheck frequencies](../data-warehouse-mgr/cfg-data-rechecks.md), and the number of dashboards and charts are just a few contributors. Adobe recommends [reconfiguring some of your settings](../../best-practices/reduce-update-cycle-time.md) and [optimizing your database for analysis](../../best-practices/opt-db-analysis.md) to reduce update times.

## Can I be notified when an update cycle completes? {#notifyupdate}

If an update is in progress, there is a link on the `Connections` page that you can use to request an email notification once the cycle completes.

## Why is[!DNL Google ECommerce]data different from my database? {#ecommdatabase}

Discrepancies between [!DNL Google Analytics] and your database can arise for various reasons. Tracking not being properly enabled, users visiting incognito, and click events not working correctly are just a few examples. If your revenue and orders do not look right, [use this article](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) to diagnose the problem.

## How do I troubleshoot a data discrepancy? {#datadiscrepancy}

Adobe knows that seeing inconsistent data can be a frustrating experience. Try using the [Data Discrepancy Checklist](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=en) or [Data Exports tutorial](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en) to diagnose the problem. If you are still stumped, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
