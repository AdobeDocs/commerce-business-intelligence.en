---
title: Supported SQL functions
description: Learn which data types and formats are supported by SQL functions.
---
# Supported SQL functions 

Any [SELECT function](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), or any function that does not mutate data, that is supported by PostgreSQL is supported in the SQL Report Builder. This includes, but is not limited to, AVG, COUNT, COUNT DISTINCT, MIN/MAX, and SUM.

Also, any JOIN type is supported but we recommend only using INNER JOIN as it is the least expensive of the JOIN types.
