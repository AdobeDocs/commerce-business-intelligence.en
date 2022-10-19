---
title: MBI Essentials vs. Pro
description: Learn how MBI Essentials differs from MBI Pro.
---
# [!DNL MBI] Essentials vs [!DNL MBI] Pro

>[!NOTE]
>
>This is archived documentation for MBI.

The following table describes what is included with Essentials and Pro.

|   | **MBI Essentials**| **MBI Pro**|
|-----|-----|-----|
| **Pre-Defined Reports**| Up to 100 | Custom |
| **Pre-Defined Dashboards**| 5-6 | Custom |
| **New Custom Report Creation**| Yes | Yes |
| **Magento Commerce Tables**| 4-6 | Unlimited |
| **Log-ins/User Accounts**| 10 | 20 |
| **User Permissions**| Yes | Yes |
| **Data Warehouse Manager**| Unavailable | Available |
| **Email Reports**| Yes | Yes |
| **Cohort Report Builder**| Yes | Yes |
| **Google Analytics Live Integration**| Yes | Unlimited  |
| **3rd Party Integrations**|  Unavailable | Available  |
| **Full API Access**|  No | Yes  |
| **Access to CS, AM, or Analysts**|  No | Yes  |
| **Professional Services**|  Available | Available  |

{style="table-layout:auto"}

_Number of tables depends on guest checkout._

**Included tables**

* `sales\_order`
* `sales\_order\_item`
* `sales\_order\_address`
* `customer\_entity`
* `customer\_group`
* `store`

## Columns Included in Essentials

Items in _italics_ are calculated fields.

* `sales_order` table
  * entity_id
  * base_grand_total
  * customer_id
  * status
  * customer_email
  * store_id
  * base_currency_code
  * billing_address_id
  * shipping_address_id
  * base_shipping_amount
  * base_tax_amount
  * coupon_code
  * created_at
  * updated_at
  * base_subtotal
  * customer_group_id
  * base_discount_amount
  * base_discount_invoiced
  * increment_id
  * _Customer's order number_
  * _Customer's first order date_
  * _Customer's lifetime number of orders_
  * _Is customer's last order?_
  * _Billing address region_
  * _Shipping address country_
  * _Customer's lifetime revenue_
  * _Seconds between customer's first order date and this order_
  * _Seconds since previous order_
  * _Store name*
  * _Customer's lifetime number of coupons_
  * _Customer's order number (previous-current)_
  * _Shipping address region_
  * _Number of items in order
  * _Billing address city_
  * _Shipping address city_
  * _Customer's group code_
  * _Customer's first order's billing region_
  * _Customer's first order's coupon_code_
  * _Customer's creation date_
  * _Billing address country_

* `sales_order_item` table
  * item_id
  * qty_ordered
  * base_price
  * name
  * order_id
  * sku
  * product_type
  * product_id
  * created_at
  * updated_at
  * parent_item_id
  * store_id
  * base_discount_amount
  * base_discount_invoiced
  * _Order's coupon_code_
  * _Order item total value (quantity * price)_
  * _Order's increment_id_
  * _Customer's email_
  * _Customer's lifetime number of orders_
  * _Store name_
  * _Customer's order number_
  * _Order's status_
  * _Customer's lifetime revenue_

* `sales_order_address` table
  * entity_id
  * city
  * region
  * country_id

* `customer_entity` table
  * entity_id
  * email
  * group_id
  * created_at
  * updated_at
  * store_id
  * _Customer's lifetime revenue_
  * _Customer's lifetime number of coupons_
  * _Customer's first order date_
  * _Customer's lifetime number of orders_
  * _Seconds since customer's first order date_
  * _Customer's first 30 day revenue_
  * _Customer's first order's billing region_
  * _Customer's first order's coupon_code_
  * _Customer's group code_
  * _Store name_

* `customer_group` table
  * customer_group_id
  * customer_group_code

* `store` table
  * store_id
  * name

Refer to the following video series to learn more about the differences between [!DNL MBI] Essentials and [!DNL MBI] Pro.

* [Essentials](https://support.magento.com/hc/en-us/articles/360005305614)
* [Pro](https://support.magento.com/hc/en-us/articles/360005373453)