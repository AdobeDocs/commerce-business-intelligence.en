---
title: Special filter operators
description: Learn about a few special operators used in filters when creating a report or creating a metric.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
---
# Filter Options

This topic explores a few special `operators` used in `filters` when [creating a report](../../tutorials/using-visual-report-builder.md){: target="_blank"} or [creating a metric](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}.

## `Filter Operators`

* `LIKE` for pattern matching. This must be used with the wildcard characters % (for a wildcard with a variable number of letters) or _ (for a wildcard single letter).  For example, the restriction `LIKE \_ake%` would return true for `Jake Stein`, `Jake Smith`, or `Fake Smith`.  It would return false for `Drake Smith`.

* `NOT LIKE` is similar to pattern matching above, but checks for which patterns do not match.

* `IS` checks if the column is `NULL`, or empty.

* `IS NOT` is similar to the `IS` operator above, but checks for non-NULL columns.

* `IN` checks for a value's presence in a comma-separated list. (for example, "Color `IN` red,orange" is the equivalent of color `equal to` red OR color `equal to` orange).

* `NOT IN` is similar to `IN` above, but checks for a value's absence.
