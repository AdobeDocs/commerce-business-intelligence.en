---
title: Does deleting a SQL report/query also delete the underlying columns from my Data Warehouse?
zendesk_id: 360016732751
---

The answer is `no`, you won’t lose any columns, regardless of how you built them.

* Columns created using the Data Warehouse Manager won’t be affected if you delete a report or query that uses them.

* Columns created using the SQL Report Builder aren’t saved to your Data Warehouse.
