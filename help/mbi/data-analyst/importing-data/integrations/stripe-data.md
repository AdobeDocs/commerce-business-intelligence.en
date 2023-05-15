---
title: Expected Stripe data
description: Explore the main data tables that you can import from Stripe into [!DNL Commerce Intelligence].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
---
# Expected [!DNL Stripe] data

After [you have connected your [!DNL Stripe] account](../integrations/stripe.md), you can use the [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields for analysis.

This article explores the main data tables that you can import from [!DNL Stripe] into [!DNL Commerce Intelligence]. After setup is completed, the following tables will be created in your Data Warehouse. Click the links in the Table Name column to learn more about the attributes in each table.

| **Table Name** | **Description** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Customer objects allow you to perform recurring charges and track multiple charges that are associated with the same customer. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | This table contains information about charges to credit and debit cards, including the amount, currency, status, customer ID, and more. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | This table contains information about a percent- or amount-off discount that you may want to apply to a customer. Coupons only apply to invoices; they do not apply to one-off charges. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | This table contains information about invoices including the amount owed, subscriptions, invoice items, any automatic proration adjustments, and more. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | This table contains the pricing information for different products and feature levels on your site. For example, you may have a $10/month plan for basic features and a $20/month plan for premium features. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | This table contains the details of subscription plans your customers belong to. Attributes include customer ID, status, canceled/ended at dates, tax percent, trial information, and more. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Events let you know about something interesting that has happened in an account. [When an interesting event occurs](https://stripe.com/docs/api/events/types), a new event object is created. For example, when a charge succeeds `charge.succeeded` event is created; or, when an invoice cannot be paid an `invoice.payment\_failed` event is created. |

{style="table-layout:auto"}

>[!NOTE]
>
>Many API requests may cause multiple events to be created. For example, if you create a subscription for a customer, you receive both a `customer.subscription.created` event and a  `charge.succeeded` event.

## Related:

* [Connecting [!DNL Stripe]](../integrations/stripe.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
