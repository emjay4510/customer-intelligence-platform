# Source System Analysis

## Overview

The Customer Intelligence Platform uses the Olist Brazilian E-Commerce dataset as the primary transactional data source.

The dataset contains customer, order, product, payment, review, seller, and location information that enables customer behavior analytics, product performance analysis, conversion funnel tracking, and retention measurement.

---

# Source Tables

## 1. Customers

Table:
olist_customers_dataset

Primary Key:
customer_id

Columns:

* customer_id
* customer_unique_id
* customer_zip_code_prefix
* customer_city
* customer_state

Purpose:
Stores customer master information and geographical details.

Business Usage:

* Customer analytics
* Retention analysis
* Regional segmentation

---

## 2. Orders

Table:
olist_orders_dataset

Primary Key:
order_id

Foreign Key:
customer_id

Columns:

* order_id
* customer_id
* order_status
* order_purchase_timestamp
* order_approved_at
* order_delivered_carrier_date
* order_delivered_customer_date
* order_estimated_delivery_date

Purpose:
Stores order lifecycle information.

Business Usage:

* Revenue analysis
* Order trend analysis
* Customer purchase behavior

---

## 3. Order Items

Table:
olist_order_items_dataset

Primary Key:
(order_id, order_item_id)

Foreign Keys:

* order_id
* product_id
* seller_id

Columns:

* order_id
* order_item_id
* product_id
* seller_id
* shipping_limit_date
* price
* freight_value

Purpose:
Stores product-level transaction details.

Business Usage:

* Product performance
* Revenue calculations
* Basket analysis

---

## 4. Products

Table:
olist_products_dataset

Primary Key:
product_id

Columns:

* product_id
* product_category_name
* product_name_lenght
* product_description_lenght
* product_photos_qty
* product_weight_g
* product_length_cm
* product_height_cm
* product_width_cm

Purpose:
Stores product catalog information.

Business Usage:

* Product analytics
* Category analysis
* Conversion metrics

---

## 5. Payments

Table:
olist_order_payments_dataset

Foreign Key:
order_id

Columns:

* order_id
* payment_sequential
* payment_type
* payment_installments
* payment_value

Purpose:
Stores payment information for orders.

Business Usage:

* Revenue analysis
* Payment method analysis
* Customer spending patterns

---

## 6. Reviews

Table:
olist_order_reviews_dataset

Primary Key:
review_id

Foreign Key:
order_id

Columns:

* review_id
* order_id
* review_score
* review_comment_title
* review_comment_message
* review_creation_date
* review_answer_timestamp

Purpose:
Stores customer feedback and satisfaction data.

Business Usage:

* Customer sentiment analysis
* Product quality monitoring
* Service quality metrics

---

## Supporting Tables

### Sellers

Table:
olist_sellers_dataset

Primary Key:
seller_id

Purpose:
Seller dimension table used for seller-level analysis.

---

### Geolocation

Table:
olist_geolocation_dataset

Purpose:
Geographical reference dataset used for regional analytics.

---

### Product Category Translation

Table:
product_category_name_translation

Purpose:
Maps Portuguese product categories to English categories.

---

# Source Relationships

Customers
↓
Orders
↓
Order Items
↓
Products

Orders
↓
Payments

Orders
↓
Reviews

Order Items
↓
Sellers

Customers
↓
Geolocation

Products
↓
Category Translation

---

# Data Engineering Considerations

Expected Challenges:

1. Duplicate records
2. Missing values
3. Schema inconsistencies
4. Data quality validation
5. Incremental loading strategy
6. Large-scale joins
7. Customer retention calculations

Mitigation Strategy:

* Medallion Architecture
* Data validation framework
* Audit logging
* Incremental processing
* Delta Lake optimizations
* Partitioned storage design
