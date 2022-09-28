---
title: Optimizing Your SQL Queries
description: Learn how to optimize your SQL queries. 
---
# Optimize your SQL queries

The SQL Report Builder allows you to query and iterate on those queries at any given time. This is useful when you need to modify a query without having to wait for an update cycle to finish before realizing a column or report you created needs updating.

Before a query is executed, [MBI estimates its cost](https://support.magento.com/hc/en-us/articles/360016730391). Cost takes into consideration the length of time and number of resources required to execute a query. If that cost is deemed to be too high or if the number of returned rows exceeds our limits, the query will not run. We put together a list of recommendations for querying your data warehouse, which will ensure you are writing the most streamlined queries possible.

## Using SELECT * or Selecting All Columns

Selecting all columns does not make for a timely, easily executed query. Queries that use SELECT * can take quite a bit of time to run, especially if your table has a large number of columns.

For this reason, we recommends you avoid using SELECT * wherever possible and only include the columns you need:

| **Instead of this...** | **Try this!** |
| ![](../../assets/Select_all_1.png) | ![](../../assets/Select_all_2.png) |

## Using Full Outer Joins

Outer joins select the entirety of both tables being joined, which will increase the computational cost of the query. This means that your query will take longer to run and is more likely to fail, as it may take longer than the execution limit to return the results.

Instead of using this type of join, consider using an inner or left join. Inner joins return results only where tHere is a columnar match between tables (for example, `order_id` exists in both a typical `customers` and `orders` table); left joins will return all results from the left (first) table along with the matching results in the right (second) table.

Take a look at how we can rewrite a FULL OUTER JOIN query:

| **Instead of this...** | **Try this!** |
| ![](../../assets/Full_Outer_Join_1.png) | ![](../../assets/Full_Outer_Join_2.png) |

As you can see, these queries are identical in every way except for the type of JOIN they use.

## Using Multiple Joins

While you can include multiple joins in your query, remember that it may drive the query's cost up. To keep from hitting the cost threshold, we recommend avoiding multiple joins where possible.

## Using Filters

Use filters whenever possible. `WHERE` and `HAVING` clauses will filter your results and give you only the data you really want.

## Using Filters in JOIN Clauses

If you are using a filter when performing a join, be sure to apply it to both tables in the join. Even if it is redundant, this will reduce the computational cost of the query and speed up the execution time.

| **Instead of this...** | **Try this!** |
| ![](../../assets/Join_filters_1.png) | ![](../../assets/Join_filters_2.png) |

## Using Operators

When writing queries, consider using the 'least expensive' operators possible. Every query has a computational cost, which is determined by the functions, operators, and filters that make up the query. Some operators require less computational effort, which makes them less expensive than other operators.

Comparison operators (>, <, =, and so on) are the least expensive, followed by [LIKE. SIMILAR TO and POSIX operators](https://www.postgresql.org/docs/9.5/functions-matching.html) which are the most expensive operators.

## Using EXISTS Versus IN

Using EXISTS versus IN depends on the type of results you are trying to return. If you are only interested in a single value, use the EXISTS clause instead of IN. IN is used in conjunction with lists of comma-separated values, which will increase the computational cost of the query.

When IN queries are run, the system must first process the subquery (the IN statement), then the entire query based on the relationship specified in the IN statement. EXISTS is far more efficient because the query does not have to be run through multiple times - a true/false value is returned while checking the relationship specified in the query.

To put it simply: the system does not have to process as much when using EXISTS.

| **Instead of this...** | **Try this!** |
| ![](../../assets/Exists_1.png) | ![](../../assets/Exists_2.png) |

## Using ORDER BY

ORDER BY is an expensive function in SQL and can significantly raise the cost of a query. If you receive an error message saying that the EXPLAIN cost of your query is too high, try eliminating any ORDER BYs from your query unless absolutely required.

This is not to say that ORDER BY can not be used - just that it should only be used when necessary.

## Using GROUP BY and ORDER BY

While there may be a few situations where this approach does not conform with what you are trying to do, the general rule is that if you are using a GROUP BY and ORDER BY, you should put the columns in both clauses in the same order. For example:

| **Instead of this...** | **Try this!** |
| ![](../../assets/Group_by_2.png) | ![](../../assets/Group_by_1.png) |

## Wrapping Up

The best way to learn to write SQL - and do so efficiently - is through trial and error. To find what works best for you, try to recreate a few reports using only the SQL editor.
