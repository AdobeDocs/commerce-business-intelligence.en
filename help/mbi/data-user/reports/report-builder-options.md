---
title: Which Report Builder should I use?
zendesk_id: 360016503932
---

>[!NOTE]
>
>[Requires Admin permissions.](../../administrator/user-management/user-management.md)

We all like having options. But, when confronted with choices, some of us might balk and freeze at the idea of having to commit to a decision. Options are great, but they can also be overwhelming and confusing.

Now that you have more options for creating analyses, it might sometimes be difficult to know exactly which flavor of the report builder will suit your needs. If you need some guidance on choosing the best way to build your analysis, this article is for you.

## When should I use the SQL Report Builder? {#whensql}

Take a look at some of the more common reasons you would use the SQL Report Builder over the traditional Report Builder.

### If you want to use SQL-specific functions…

Part of the beauty of the SQL Report Builder is that it gives you the ability to use functions that are not currently available in the Data Warehouse Manager. In the past, an analyst may have had to step in to help you fully realize your vision.

The SQL Report Builder supports functions like [LISTAGG](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) and [GETDATE](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), which you could not previously use. You can access the [full list](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), but some other SQL-specific functions include:

* [Bitwise aggregate functions](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [CASE expression](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [JSON_EXTRACT_PATH_TEXT](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [LOG](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [MONTHS_BETWEEN](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [REPLACE](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [SQRT](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [&#124;&#124; (concatenation) operator](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### If you want to do some testing…

If you want to try different techniques and strategies to figure out what works best for your analysis, you might want to use the SQL Report Builder. Building out columns in the Data Warehouse Manager takes time and columns you create using the DWM are dependent on update cycles.

At best, you'll have to wait through one update cycle before you can use your column. If you realize you made a mistake in building the column, you'll have to wait through **two** cycles: one to initially populate the column, and another cycle for the revisions to propagate.

### If you will only use a new column once…

As we mentioned in the section above, creating a new column in the Data Warehouse Manager takes time. If you only plan on using a column you create in one report, we suggest using the SQL Report Builder. This will eliminate the need to wait for an update cycle to complete, getting you back to work more quickly.

### If you are working with data that has a one-to-many relationship…

In some cases, the structure of your data might make the SQL Report Builder a more efficient and logical choice to build your analysis. Creating columns for one-to-one relationships is pretty straightforward in the Data Warehouse Manager, but things can get a little confusing when you're dealing with one-to-many relationships.

Let's say a single product is considered a part of multiple product categories, and you would like to view the revenue associated with each category of each product. Trying to create this relationship using the DWM can be tedious and difficult, but writing a SQL query may be a bit more straightforward:

![](../../assets/When_should_I_use_the_RB_2.png)

## When should I use the traditional Report Builder? {#whentraditionalrb}

While the SQL Report Builder gives you more control and access to previously unavailable functionality, it might not always be the right choice. We suggest that you also consider the following when deciding what flavor of the report builder to use.

### If you are building a simple report…

If what you want to create is straightforward, using the traditional Report Builder can be much faster than writing a full SQL query. It will also help if any columns you need to create the analysis are already in the Data Warehouse Manager.

### If you will be sharing your work with other users…

Will users across your organization be using/viewing this analysis? Depending on who you are sharing your work with, sticking with the Visual Report Builder may be better in some cases. Users can quickly look at the definition in the Visual Report Builder versus reading a potentially long SQL query.

If there are some people who need the report but are not familiar with SQL, we recommend using the original flavor of the Report Builder. It will make things easier on them.

## Wrapping up {#wrapup}

Both the SQL and Visual Report Builders are suitable for a wide variety of use cases. This typically depends on what your analytical needs are and who will be consuming the analysis.
