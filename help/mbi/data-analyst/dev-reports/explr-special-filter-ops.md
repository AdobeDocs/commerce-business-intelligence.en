---
title: Special filter operators
description: Learn about a few special operators used in filters when creating a report or creating a metric.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw
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
