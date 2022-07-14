---
title: What SQL functions are supported?
zendesk_id: 360016733091
---

Any [SELECT function](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), or any function that doesn't mutate data, that's supported by PostgreSQL is supported in the SQL Report Builder. This includes, but isn’t limited to, AVG, COUNT, COUNT DISTINCT, MIN/MAX, and SUM.

Also, any JOIN type is supported but we recommend only using INNER JOIN as it's the least expensive of the JOIN types.
