---
title: Expected QuickBooks data
description: Learn how to easily track relevant data fields for analysis.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
---
# Expected [!DNL QuickBooks] data

After [you have connected your [!DNL QuickBooks] account](../../../data-analyst/importing-data/integrations/quickbooks.md), you can use the [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) to easily track relevant data fields for analysis. The following tables are created in your Data Warehouse:

To view all the fields available for tracking, click the links in the table name column.

## Transaction Entities {#transactionentities}

| **Table Name** | **Description** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | The `bills` table contains information about AP transactions, or a request for payment from a third party. Attributes include currency type, exchange rate, total amount, due date, balance, and more. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` entities are the final transaction of payment of bills received from a vendor. This table includes the vendor information, payment type, total amount, transaction date, and more. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | The `creditmemos` table records transactions that are refunds or credits of both full and partial payments. Some attributes include the customer's name, the customer's billing and shipping info, the amount, and date. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` include direct deposits and customer payments moved into the Asset Account after being held in the `Undeposited Funds` account. Attributes include the amount, deposit ID, and date. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` are transactions given to customers that include proposed pricing for a good or service. This table records the amount, any discount information, customer information, and date. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` are sales forms that a customer pays later. The invoices table records any deposit information, date, line items, tax information, and customer information. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | The `journalentries` table records AR and AP account information, including the journal entry ID, transaction date, and line item information. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | A `payment` record includes attributes such as the payment ID, applied and unapplied amounts, transaction date, transaction type, and processing status. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | The `purchases` table represents your expenses and includes the purchase ID, payment type, amount, and any line item information. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | The `purchaseorders` table holds requests for goods sent to vendors. This table includes the vendor information, purchase order ID, transaction date, line item information, total amount, and AP account information. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | The `refundreceipts` table records refunds given to customers. Attributes include the refundreceipt ID, line item information, total amount, customer information, and balance. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | The `salesreceipts` table records information in the sales receipts given to customers, including the salesreceipt ID, line item information, total amount, customer information, transaction date, and any deposits. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | The `timeactivities` table holds time records for vendors and/or employees and includes the time activity ID, employee/vendor information, time logged, activity description, and date recorded. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | The `transfers` table records information on funds moved between accounts. Attributes include the transfer ID, amount, account information, and date. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Vendor credits are AP transactions that are refunds or credits given to vendors. The `vendorcredits` table includes the vendor credit ID, line item information, vendor information, AP account, total amount, and date. |

{style="table-layout:auto"}

## Name List Entities {#namelistentities}

| **Table Name** | **Description** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | This table includes the account ID, name, status, type, balance, currency, and creation time. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | This table records all information relating to company budgets, including the budget ID, name, start and end dates, type, status, and details. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | Classes, applied to detail lines of transactions, allow you to track segments that are not tied to a client or project. This table records the class ID, name, subclass, and status. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | The `customers` table holds all information relating to your customers, including the customer's ID, name, billing and shipping addresses, phone number, and email address. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | The `departments` table includes the department ID, name, and type (subdepartment vs top-level department). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | The `employees` table records information about the people who work for your company. Attributes include the employee ID, name, address, phone number, and billable information, if the company is payroll-enabled. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | The `items` table contains details on products or services that your company sells. This table includes the item ID, name, description, unit price, type, purchasing information, on-hand quantity, and income and asset account information. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | The `paymentmethods` table records the method of payment received for goods and services. It contains the payment ID, type, and name. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | This table records information about tax agencies, including the tax agency ID, and tracking information on taxes for purchases and sales. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Tax codes are used to track the tax status (taxable vs non-taxable) of products, services, and customers. The `taxcodes` table includes the tax code ID, name, description, status, taxable status, tax rate, and tax group. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Tax rates are used to calculate tax liabilities. This table includes the tax rate ID, name, description, rate, tax agency, and more. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | This entity represents the terms under which sales are made. The terms table includes the term ID, name, type, discount percent, and due days. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | The vendors table contains information about the vendors you purchase from. Table attributes include the vendor ID, company name, account number, account balance, 1099 status, billing address, phone number, email address, and web address. |

{style="table-layout:auto"}

## Related:

* [Connecting [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Reauthenticating integrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
