---
title: Consolidating your Tables
zendesk_id: 360016504572
---

If you operate multiple store fronts or in multiple markets, you may have similar databases stored separately. In MBI, it is easy to consolidate similar tables from different databases together.

For example, you may have an `orders` table for Market A, and a similar `orders` table for Market B. MBI can consolidate both tables and allow you to look at the aggregate order data from both Market A and B, in addition to segmenting it by specific market.

For consolidation of tables to work, input tables must be **similarly structured**. In other words, all input tables must contain the data columns required in the consolidated table.

This topic discusses some of the most common use cases for consolidated tables and the next steps required for creating your own.

## Recommendations for When to Use Consolidated Tables

The following sections discuss when it might be appropriate to use consolidated tables in your system.

### Integrating Data from Multiple Websites

If you sell your products under different brands and websites, it's likely that the tables for each brand or website are similarly structured.

For example, you may have an `orders` table for website A and a separate, but similar, `orders` table for website B. In this situation, it may be useful to consolidate the `orders` tables from website A and B so that you can look at the consolidated revenue and number of orders from website A and B, in addition to be able to segment metrics by these two websites.

### Integrating Legacy Data

Many companies have refactored their databases at one time or another, and the data from the old database does not always get converted over to the new system. You can use consolidated tables to join the key columns from legacy tables with those from the active system. This allows you to conduct a unified analysis of your data throughout history.

### Combining Events for Active User Analysis

Imagine a website where users can do several things: take a survey, play a game, make a purchase, refer a friend, and so on. Typically, each of these events will be stored in its own table. This makes it difficult to conduct an analysis of how many distinct users took at least one action of any kind in a given time period.

You can utilize consolidated tables to create one unified list of all users and when any of these events took place. You can then run queries on the consolidated table to easily conduct such an analysis.

As with all other tables in your data warehouse, you can add additional columns to power different kinds of charts and analyses.

## Creating, Viewing, or Updating a Consolidated Table

If you are interested in adding a consolidated table to your data warehouse, contact MBI [support](../../getting-started/support.md).

Likewise, because consolidated tables are not viewable in the Data Warehouse Manager, viewing and updating these tables can only be done by MBI support.
