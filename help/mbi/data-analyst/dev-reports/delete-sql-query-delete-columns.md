---
title: Does deleting a SQL report/query also delete the underlying columns from my Data Warehouse?
zendesk_id: 360016732751
---

The answer is `no`, you will not lose any columns, regardless of how you built them.

* Columns created using the Data Warehouse Manager will not be affected if you delete a report or query that uses them.

* Columns created using the SQL Report Builder are not saved to your Data Warehouse.
