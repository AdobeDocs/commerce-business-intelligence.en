---
title: New Architecture
description: Learn about the benefits of moving to new architecture.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: 
---
# New Architecture

[!DNL Adobe Commerce Intelligence] Product and Engineering teams have been focused on making the most sweeping, highly requested improvements possible for the last year. Adobe is thrilled to announce the availability of a new [!DNL Commerce Intelligence] product architecture that makes these improvements a reality.

## Benefits of New Architecture

* Create types of columns in the Data Warehouse, including calculated columns with SQL.
* New columns are available immediately.
* Data latency is dramatically improved.

## Technical Benefits

The main differences are listed above, but the main change is the way calculations are performed during the update cycle. Calculations are no longer run on every column during every update; they are instead run on-demand from the Visual Report Builder.

### Moving to New Architecture

As the accounts are fundamentally built differently, there is no automatic process to migrate your Data Warehouse or reports to a new architecture account. Moving to the new architecture requires a re-implementation of your existing account.

### Cost to Move to the New Architecture

No added cost! Adobe will create this new account for you to begin re-implementation, which is free for at least one month. This allows you time to have both accounts open so that you can more easily perform the re-implementation and ensures that your team does not have a gap in service.

### Time Needed to Reimplement Account in the New Architecture

Re-implementation times vary depending on what you want to rebuild. Adobe recommends that you perform the following steps in your existing account to get an idea of what would be involved in your re-implementation:

* Identify a core set of reports/dashboards.
* Identify metrics and dimensions required to build those reports.
* Identify the columns required to recreate those metrics and dimensions.

When this is complete, you know what data you need to sync to the new architecture Data Warehouse in order to rebuild those core reports.

### Getting Help

The [!DNL Adobe Commerce Intelligence] [Services team](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) can perform your re-implementation for an extra cost. Contact your [Adobe Account Team](../../guide-overview.md#Submitting-a-Support-Ticket) and be prepared to provide a list of dashboards/reports that you want to prioritize creating in the new account

### Staying with Existing Architecture

If these features are not important to you, you can stick with your existing account. There is no extra cost for keeping your existing account. Adobe continues supporting those accounts with no changes.
