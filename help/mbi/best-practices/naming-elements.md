---
title: Name reports and elements in Commerce Intelligence
description: Learn best practices for naming reports and elements in [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
---
# Name reports and elements

Before you get started building in [!DNL Adobe Commerce Intelligence], Adobe wants to share some secrets to success. Knowing how to create metrics, filters, and so on, is important, but all your work may be for naught if you cannot find what you need or if there is ambiguity.

## Why is nomenclature important? {#why}

The way you name your calculated columns, metrics, and reports dictates the ease in which different users can navigate through your [!DNL Commerce Intelligence] account. When naming these features, keep in mind the three Cs:

* **CLARITY** - So you can tell at a glance what a report is showing, what a metric does, and so on.
* **CONSISTENCY** - So that you (and the Adobe support team) can easily find and understand elements and reports in your account.
* **CREDIBILITY** - In order to inspire and empower other data-driven [!DNL Commerce Intelligence] users, you need to instill confidence in how they understand and use the data!

Read on for tried and true nomenclature tips!

## General best practices {#general}

### Be meaningful {#meaningful}

Be specific whenever possible! For example, if it is the country, do you know if it is the shipping or the billing country? Is it the user's city, or it is the deal's city?

**Bad example:**
 Revenue

This is vague and does not tell us much.

**Good examples:**
 Revenue (base grand total + fee)
 User's shipping country

These examples are specific, which decreases the potential for confusion.

### Be consistent with capitalization {#capitalize}

[!DNL Adobe] recommends first letter uppercase with the rest of the characters lowercase, unless proper noun style of capitalization. For example, **User's order number** rather than **User's Order Number.**

This is really a matter of preference, but the thing to remember is to be consistent with whatever you choose.

### Entity consistency {#entity}

You likely already have a nomenclature in place at your company. Keep the metrics and dimensions that you put in place consistent with what is used in other databases and tools. For example:

* User vs. Customer vs. Member vs. Account
* Company vs. Account vs. Organization
* Registration vs. Creation

### Spelling and grammar {#spelling}

Make sure to double-check your spelling and do not forget about those pesky possessives!

## Charts {#charts}

When naming [charts](../tutorials/using-visual-report-builder.md), it is most useful to follow this formula: **(Data Perspective) + (Metric) + (Time Period) + (Time Interval)**

**Bad example:**
 Revenue

This tells us nothing about the report, which is bad.

**Good example:**
 Cumulative revenue past 30 days by month

This tells us **exactly** what is in the report, which is fantastic.

## Dashboards {#dashboards}

Dashboards should be named in ways that thematically represent the reports contained within them. For example, if your dashboard contains only information related to revenue and orders, consider naming it something like **Store Name - Revenue and orders.**

Conversely, if your dashboard is a place where you are experimenting with different reports, consider naming it **Your Name's Sandbox** so you know that the reports contained within are drafts.

## Dimensions (Calculated columns) {#dimensions}

When naming new [dimensions](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), it is most useful to follow this formula: **(Entity) + (Nth) + (time frame) + (calculation) + (comments)**. For example:

User's first 30-day revenue
* User's order number
* User's order number (awaiting audit)

## Filter Sets {#filterset}

[Filter sets](../data-user/reports/ess-manage-data-filters.md) are typically named in ways that explain the information they are including or excluding. For example, naming a filter set **Order items we count** allows any user to go in, view the logic of the filter set, and understand what order information determines what is counted across the business. Remember that filter sets can be applied to both calculated columns and metrics, and should be easy to understand.

## Metrics {#metrics}

[Metrics](../data-user/reports/ess-manage-data-metrics.md) are essentially questions that you want answers to regularly. What was the number of orders in the past month? What is the average lifetime value of your customers? It is best practice to name metrics to reflect the answer they are giving users. Also, if you have the same metric filtered for a specific store or department, they should be labelled as such. For example:

Average customer LTV (first 30 days)
 Store Name - Revenue

Finally, the same metric can sometimes be organized by different timestamps, depending on how individual users calculate it. If so, make sure to include the timestamp in the name:

Revenue (shipped\_at)
 Revenue (created\_at)

## Wrapping Up {#wrapup}

Establishing style and naming conventions early helps set you up for success in your [!DNL Commerce Intelligence] account. Remember the three Cs: clarity, consistency, and credibility.
