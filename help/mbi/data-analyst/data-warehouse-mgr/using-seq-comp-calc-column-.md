---
title: Using the Sequential Comparison Calculated Column
zendesk_id: 360016503112
---

This topic outlines the purpose and uses of the **Sequential Comparison** calculated column available in the **Manage Data** > **Data Warehouse** page. Below is an explanation of what it does, followed by an example, and the mechanics of creating it.

**Explanation**

The **Sequential Comparison** column type finds the difference between consecutive events. The most common type of **Sequential Comparison** column is the **Seconds since previous order** column. There are three inputs needed for this column:

1. **Event Owner**: This input determines the entity for which rows are grouped. For example, in the **Seconds since previous order** column, the event owner is the customer, because we want to find the number of seconds since the previous order of the same customer.
1. **Event Date**: This input enforces the sequence of events. In the case of **Seconds since previous order**, the column containing the timestamp of the order should be the **Event Date**. This input is always a timestamp.
1. **Value to Compare**: This input is the actual value to be compared. It subtracts the previous row's value from the current row's value. Hence, a column finding the time difference between successive orders of a customer is called **Seconds since previous order**. This input does not have to be a timestamp. A non-timestamp example is to find the difference in order value between successive orders of a customer.

**Example**

<table style="width: 693px; height: 283px;">
<tbody>
<tr style="height: 49px;">
<td style="height: 49px; width: 80px;">
<p><strong>event_id</strong> </p>
</td>
<td style="height: 49px; width: 86px;">
<p><strong>owner_id</strong> </p>
</td>
<td style="height: 49px; width: 173px;">
<p><strong>timestamp</strong> </p>
</td>
<td style="height: 49px; width: 341px;">
<p><strong>Seconds since owner's previous event</strong> </p>
</td>
</tr>
<tr style="height: 49px;">
<td style="height: 49px; width: 80px;">
<p><strong>1</strong> </p>
</td>
<td style="height: 49px; width: 86px;">
<p>A </p>
</td>
<td style="height: 49px; width: 173px;">
<p>2015-01-01 00:00:00 </p>
</td>
<td style="height: 49px; width: 341px;">
<p>NULL </p>
</td>
</tr>
<tr style="height: 49px;">
<td style="height: 49px; width: 80px;">
<p><strong>2</strong> </p>
</td>
<td style="height: 49px; width: 86px;">
<p>B </p>
</td>
<td style="height: 49px; width: 173px;">
<p>2015-01-01 00:30:00 </p>
</td>
<td style="height: 49px; width: 341px;">
<p>NULL </p>
</td>
</tr>
<tr style="height: 49px;">
<td style="height: 49px; width: 80px;">
<p><strong>3</strong> </p>
</td>
<td style="height: 49px; width: 86px;">
<p>A </p>
</td>
<td style="height: 49px; width: 173px;">
<p>2015-01-01 02:00:00 </p>
</td>
<td style="height: 49px; width: 341px;">
<p>7200 </p>
</td>
</tr>
<tr style="height: 49px;">
<td style="height: 49px; width: 80px;">
<p><strong>4</strong> </p>
</td>
<td style="height: 49px; width: 86px;">
<p>A </p>
</td>
<td style="height: 49px; width: 173px;">
<p>2015-01-02 13:00:00 </p>
</td>
<td style="height: 49px; width: 341px;">
<p>126000 </p>
</td>
</tr>
<tr style="height: 18px;">
<td style="height: 18px; width: 80px;">
<p><strong>5</strong> </p>
</td>
<td style="height: 18px; width: 86px;">
<p>B </p>
</td>
<td style="height: 18px; width: 173px;">
<p>2015-01-03 13:00:00 </p>
</td>
<td style="height: 18px; width: 341px;">
<p>217800 </p>
</td>
</tr>
</tbody>
</table>

 In the above example, **Seconds since owner's previous event** is the **Sequential Comparison** calculated column. For the **owner_id** = A, it first identifies a sequence based on the **timestamp** column, and then subtracts the previous event's **timestamp** from the current event's timestamp. In the 3rd row in the table – the 2nd row for **owner_id** A – the value of **Seconds since owner's previous event** is the number of seconds between '2015-01-01 02:00' and '2015-01-01 00:00:00'. This difference equals 2 hours = 7200 seconds.

For this calculated column type, the row corresponding to the owner's first event has a NULL value.

**Mechanics**

To create an **Event Number** column:

1. Navigate to the **Manage Data** > **Data Warehouse** page.
1. Navigate to the table on which you want to create this column.
1. Click the green **Create New Column** button at the top right of the screen.
1. Select **Same Table** as the Definition Type (if the columns you want to compare are not on the same table you may need to relocate them).
1. Select **SEQUENTIAL_COMPARISON** as the Column Definition Equation.
1. Choose the inputs, as explained above:
   - Event Owner
   - Event Date
   - Value to Compare
1. Filters can also be added to exclude rows from being considered. The excluded rows will have a NULL value for this column.
1. Provide a name for the column at the top of the page and click **Save**.
1. The column will be available to use immediately.

![SEC_new.png](../../assets/SEC_new.png){: width="665" height="492"}
