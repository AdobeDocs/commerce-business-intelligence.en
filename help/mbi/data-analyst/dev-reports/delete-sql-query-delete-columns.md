---
title: Deleting a SQL report/query
description: Learn whether or not deleting a SQL report also deletes underlying columns from my Data Warehouse.
---
# Does deleting a SQL report also delete the underlying columns from my Data Warehouse?

The answer is `no`, you will not lose any columns, regardless of how you built them.

* Columns created using the Data Warehouse Manager will not be affected if you delete a report or query that uses them.

* Columns created using the SQL Report Builder are not saved to your Data Warehouse.
