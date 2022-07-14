---
title: New Architecture
zendesk_id: 360016503052
---

Our Product and Engineering teams have been focused on making the most sweeping, highly-requested improvements possible for the last year. We are thrilled to announce the availability of a new Magento BI product architecture that makes these improvements a reality.

## Benefits of New Architecture

* Create new types of columns in the data warehouse, including calculated columns with SQL
* New columns are available immediately
* Data latency is dramatically improved

## Technical Benefits

The main differences are listed above, but what has technically changed is the way we perform calculations during the update cycle. Calculations are no longer run on every column during every update; they are instead run on-demand from the Visual Report Builder.

### Moving to New Architecture

As the accounts are fundamentally built differently, there is no automatic process we can employ to “migrate” your data warehouse or reports to a new architecture account, so moving to the new architecture requires a re-implementation of your existing account.

### Cost to Move to the New Architecture

No added cost! We will create a new account for you to begin re-implementation, which is free for at least one month. This allows you time to have both accounts open so that you can more easily perform the reimplementation and ensures that your team won’t have a gap in service.

### Time Needed to Re-implement Account in the New Architecture

Reimplementation times vary depending on what you want to rebuild. We recommend that you perform the following steps in your existing account to get an idea of what would be involved in your re-implementation:

  * Identify a core set of reports/dashboards
  * Identify metrics and dimensions required to build those reports
  * Identify the columns required to recreate those metrics and dimensions

When this is complete, you will know what data you need to sync to the new architecture data warehouse in order to rebuild those core reports.

### Getting Help

The Magento BI Services team can perform your re-implementation for an additional cost. Contact our [Customer Success team]({% link getting-started/support.md %}) and be prepared to provide a list of dashboards/reports that you want to prioritize creating in the new account

### Staying with Existing Architecture

If these features aren’t important to you, you can stick with your existing account. There is no added cost for keeping your existing account, and we will continue supporting those accounts with no changes.
