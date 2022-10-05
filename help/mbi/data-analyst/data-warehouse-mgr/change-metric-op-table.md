---
title: Change a metric's operational table
description: Learn how to change the data table that a metric uses to perform its operation.
---
# Change a metric's operational table

In certain cases, you may decide to change the data table that a metric uses to perform its operation. For example, if you have a new users table, you will want to migrate your user related metrics from the  "Users\_Old" table to use the "Users\_New" table instead.

1. Go to Data > Metrics
1. Click **Edit** beside the metric for which you would like to switch the operational table.
1. In the editor, click **Change**.

    ![](../../mbi/assets//2013-08-01_1412.png)
1. Now select the new table that you would like to base this metric on.
1. Next, you will have to match existing data dimensions to corresponding ones in the new table. For example, if you had a column called "User's registration date", simply select which column in the new table records the same date data. **(See next step if you do not have matching columns in the new table)**

    ![](../../mbi/assets//2013-08-01_1414.png)
1. If you do not have a matching column in the new table, you can either **create it in your data table** ([contact support](../../getting-started/support.md) if it is a calculation column or dimension made by MBI), or simply **delete the dimension from the metric**. To delete a dimension that you no longer need, simply go back to the metric's editor and select which dimensions to delete under "Dimensions".

    ![](../../mbi/assets//2013-08-01_1419.png)
