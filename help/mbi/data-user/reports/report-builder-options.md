---
title: Choose a report builder
description: Learn how to choose your report builder.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/xXSDN9dKTWp8SdeZHBmDYZhnNbxn8F-D6UvKa4qJlCI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Choose a report builder

>[!NOTE]
>>Requires [Admin permissions](../../administrator/user-management/user-management.md).

Now that you have more options for creating analyses, it may sometimes be difficult to know exactly which flavor of the report builder suits your needs. This topic guides you through choosing the best way to build your analysis.

## When should I use the [!DNL SQL Report Builder]? {#whensql}

Look at some of the more common reasons that you would use the [!DNL SQL Report Builder] over the [!DNL traditional Report Builder].

### If you want to use [!DNL SQL]-specific functions…

Part of the beauty of the [!DNL SQL Report Builder] is that it gives you the ability to use functions that are not currently available in the Data Warehouse Manager. In the past, an analyst may have had to step in to help you fully realize your vision.

The [!DNL SQL Report Builder] supports functions like [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) and [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), which you could not previously use. You can access the [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), but some other SQL-specific functions include:

* [`Bitwise aggregate` functions](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operator](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### If you want to do some testing…

If you want to try different techniques and strategies to figure out what works best for your analysis, you might want to use the [!DNL SQL Report Builder]. Building out columns in the Data Warehouse Manager takes time and columns that you create using the DWM depend on update cycles.

At best, you must wait through one update cycle before you can use your column. If you realize you made a mistake in building the column, you have to wait through *two* cycles: one to initially populate the column, and another cycle for the revisions to propagate.

### If you only use a new column once…

As mentioned in the section above, creating a column in the Data Warehouse Manager takes time. If you only plan on using a column you create in one report, Adobe suggests using the [!DNL SQL Report Builder]. This eliminates the need to wait for an update cycle to complete, getting you back to work more quickly.

### If you are working with data that has a one-to-many relationship…

Sometimes, the structure of your data might make the [!DNL SQL Report Builder] a more efficient and logical choice to build your analysis. Creating columns for one-to-one relationships is straightforward in the Data Warehouse Manager, but things can get a little confusing when you are dealing with one-to-many relationships.

Say that a single product is considered a part of multiple product categories, and you would like to view the revenue associated with each category of each product. Trying to create this relationship using the DWM can be tedious and difficult, but writing a [!DNL SQL] query may be a bit more straightforward:

![SQL query showing revenue by product category with one-to-many relationships](../../assets/When_should_I_use_the_RB_2.png)

## When should I use the traditional Report Builder? {#whentraditionalrb}

While the [!DNL SQL Report Builder] gives you more control and access to previously unavailable functionality, it might not always be the right choice. Adobe suggests that you also consider the following when deciding what flavor of the report builder to use.

### If you are building a simple report…

If what you want to create is straightforward, using the traditional Report Builder can be much faster than writing a full [!DNL SQL] query. It helps if any columns that you need to create the analysis are already in the Data Warehouse Manager.

### If you are sharing your work with other users…

Are users across your organization using/viewing this analysis? Depending on who you are sharing your work with, sticking with the Visual Report Builder may be better sometimes. Users can quickly look at the definition in the [!DNL Visual Report Builder] versus reading a potentially long [!DNL SQL] query.

If there are some people who need the report but are not familiar with [!DNL SQL], Adobe suggests using the original flavor of the Report Builder. It makes things easier on them.

## Wrapping up {#wrapup}

Both the [!DNL SQL Report Builder] and [!DNL Visual Report Builder] are suitable for a wide variety of use cases. This typically depends on what your analytical needs are and who are consuming the analysis.
