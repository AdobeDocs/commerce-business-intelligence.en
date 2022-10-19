---
title: Understand your [!DNL MBI] Environment
description: Learn about working with and improving your [!DNL MBI] environment. 
---
# Your [!DNL MBI] Environment

As you analyze your Commerce data, be aware of these factors and common misconceptions. If you need assistance with making sure you are using your Magento schema correctly, do not hesitate to [contact support](../getting-started/support.md).

## entity\_id

Many of your tables contain a column named `entity\_id`. In each table that contains an `entity\_id`, that column is used to identify unique rows.

For example, each row in the `sales\_order` table is a unique order. The primary key in this table is called `entity\_id`. This column can be thought of as `order\_id`. In a separate table, `customer\_entity`, each row represents a unique customer. The primary key in this table is also called `entity\_id`, which can be thought of as `customer\_id`.

In those tables, `sales\_order.entity\_id` does not equal `customer\_entity.entity\_id`. This holds true for all sets of tables that contain `entity\_id`: `table\_A.entity\_id` does not equal `table\_B.entity\_id`.

## Guest orders

If you allow customers to order from your site without having an account (guest orders), those customers will not populate as a row in your `customer\_entity` table. Additionally, each order placed by a guest will have a null `customer\_id` value on the `sales\_order` table.

Therefore, if you wish to track your guests' behaviors over time, all customer-level columns must to be calculated on the `sales\_order` table, using a customer identifier such as `customer\_email`.

If you utilize the `sales\_order` table as a customer table, you must then be careful when creating customer-level metrics. For example, consider an average lifetime revenue metric. This metric is used to identify the average lifetime revenue across your customer base. This first requires a new column that, for each customer, returns their lifetime revenue. Then you must average this column to obtain your customers' average lifetime revenue.

If you are able to use the `customer\_entity` table, each row is a single customer, and each customer only exists in that table one time. Therefore, when you have the lifetime revenue column, all you need is to create an average metric. However, if you use the `sales\_order` table as your customer table, a customer can potentially exist in numerous rows. After setting up the lifetime revenue column, each order (row) placed by a given customer will show that customer's lifetime revenue; but you only want to include that customer once in your overall average metric.

The trick here is that you must add a filter to your metric that ensures you only include each customer one time. We encourage you to create and use a filter set called **Customers we count** that will filter for **Customer's order number = 1** (among other filters you may need to exclude unwanted customers). Adding this filter ensures you will only include each customer one time in a customer-level metric.

## Products and categories

Products can have multiple categories, and categories can be used for more than one product. Therefore, when setting up category-level analyses, you must be careful to use the correct definitions. Do you want the top level category? Second level category? What if the product can fall into multiple top level categories?

Imagine a pair of jeans that falls into three different category levels, as defined by a Magento implementation: 'Clothing' (top level), 'Outerwear' (second level), and 'Pants' (third level). You might wish to analyze your categories performance by number of units sold. The metric you will need for this analysis is _Items sold_, which is built on the `sales\_order\_item` table. Therefore, you need to move category-level information onto the items table. Each row on the `sales\_order\_item` table will have an associated `product\_id`, so if you know the categories associated with a product, you can bring that information over to the desired table.

Before moving any data, you must first know the proper joins and filters to ensure you grab the correct category. For some analyses, you may need to know 'Pants', but in other analyses, 'Clothing' might be more appropriate. These are distinct categories that are identified separately. Knowing how each category level is defined will ensure you are able to attribute unit sales to the appropriate category for your specific analysis.

Now, imagine you also have an 'Our Favorites' top level category on the home page of your website. Perhaps you have implemented your Magento store to include these jeans in both the 'Clothing' category as well as the 'Our Favorites' category. If so, then this pair of jeans will have more than one top level category. In that case, moving a single top level category over to the `sales\_order\_item` table does not quite make sense, as there are multiple options. To account for this, we suggest creating yes/no columns that check for specific categories. For example, `Is product in Clothing category?` and `Is product in Our Favorites category?` columns will allow you to check if a product falls into those specific categories.
