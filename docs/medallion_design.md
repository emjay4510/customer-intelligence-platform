# Medallion Architecture

## Bronze Layer

Raw ingested data.

Tables:
- bronze_customers
- bronze_orders
- bronze_order_items
- bronze_products
- bronze_reviews
- bronze_clickstream

---

## Silver Layer

Validated and cleansed data.

Tables:
- silver_customers
- silver_orders
- silver_customer_orders
- silver_products
- silver_sessions

---

## Gold Layer

Business-ready analytics.

Tables:
- gold_sales_summary
- gold_customer_retention
- gold_product_performance
- gold_customer_funnel
- gold_session_analytics