---
title: Using the Event Number Calculated Column
zendesk_id: 360016503152
---

This topic outlines the purpose and uses of the **Event Number** calculated column available in the **Manage Data** > **Data Warehouse** page. Below is an explanation of what it does, followed by an example, and the mechanics of creating it.

**Explanation**

The **Event Number** column type identifies the sequence in which events occurred for a particular **event owner**, like a customer or user. If you are familiar with SQL, this column type is identical to the **RANK** function. It could be used to observe differences in behavior between first-time events, repeat events, or nth events in your data.

In case of ties, this column contains the same **rank** for the tied events, and skips the subsequent numbers. For example, if it were ranking the numbers 5,8,10,10,12, the ranks would be 1,2,3,3,5.

The most common use case of this column is to analyze first time buyers and repeat buyers. First time buyers are identified by adding a filter (to a metric or report) on **Customer's order number** = 1. **Customer's order number** is a column of the type **Event Number**.

**Example**

|||||
|--- |--- |--- |--- |
|**event_id**|**owner_id**|**timestamp**|**Owner's event number**|
|**1|A|2015-01-01 00:00:00|1|
|**2|B|2015-01-01 00:30:00|1|
|**3|A|2015-01-01 02:00:00|2|
|**4|A|2015-01-02 13:00:00|3|
|**5|B|2015-01-03 13:00:00|2|

<!--<table style="height: 173px;" width="734">
<tbody>
<tr>
<td style="width: 113px;">
<p>**event_id</strong> </p>
</td>
<td style="width: 122px;">
<p>**owner_id</strong> </p>
</td>
<td style="width: 232px;">
<p>**timestamp</strong> </p>
</td>
<td style="width: 254px;">
<p>**Owner's event number</strong> </p>
</td>
</tr>
<tr>
<td style="width: 113px;">
<p>**1</strong> </p>
</td>
<td style="width: 122px;">
<p>A </p>
</td>
<td style="width: 232px;">
<p>2015-01-01 00:00:00 </p>
</td>
<td style="width: 254px;">
<p>1 </p>
</td>
</tr>
<tr>
<td style="width: 113px;">
<p>**2</strong> </p>
</td>
<td style="width: 122px;">
<p>B </p>
</td>
<td style="width: 232px;">
<p>2015-01-01 00:30:00 </p>
</td>
<td style="width: 254px;">
<p>1 </p>
</td>
</tr>
<tr>
<td style="width: 113px;">
<p>**3</strong> </p>
</td>
<td style="width: 122px;">
<p>A </p>
</td>
<td style="width: 232px;">
<p>2015-01-01 02:00:00 </p>
</td>
<td style="width: 254px;">
<p>2 </p>
</td>
</tr>
<tr>
<td style="width: 113px;">
<p>**4</strong> </p>
</td>
<td style="width: 122px;">
<p>A </p>
</td>
<td style="width: 232px;">
<p>2015-01-02 13:00:00 </p>
</td>
<td style="width: 254px;">
<p>3 </p>
</td>
</tr>
<tr>
<td style="width: 113px;">
<p>**5</strong> </p>
</td>
<td style="width: 122px;">
<p>B </p>
</td>
<td style="width: 232px;">
<p>2015-01-03 13:00:00 </p>
</td>
<td style="width: 254px;">
<p>2 </p>
</td>
</tr>
</tbody>
</table>-->

In the above example, the column **Owner's event number** is an **Event Number** column. It ranks the owner's events in the order in which they occurred (based on the **timestamp** column).

For instance, consider all rows where **owner_id** = A. The first row in the table is the earliest timestamp for this owner, followed by the third row in the table, followed by the fourth row in the table.

**Mechanics**

Here are some instructions on creating an **Event Number** column:

1. Navigate to the **Manage Data -&gt; Data Warehouse** page.
1. Navigate to the table on which you want to create this column.
1. Click **Create a Column** and choose the **EVENT_NUMBER (…)** column type under the **Same Table** section.
1. The first dropdown **Event Owner** specifies the entity for which the rank is to be determined. In the case of **Customer's order number**, a customer identifier such as **customer_id** or **customer_email** would be the **Event Owner**.
1. The second dropdown **Event Rank** specifies the column that enforces the sequence that determines the rank of the row. In the case of **Customer's order number**, the **created_at** timestamp would be the **Event Rank**.
1. Under the **Options** dropdown, you can add filters to exclude rows from being considered. The excluded rows will have a NULL value for this column.
1. Provide a name to the column and click **Save**.
1. The column will be available to use _immediately._
