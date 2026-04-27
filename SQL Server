-- =========================================
-- RETAIL SALES ANALYSIS PROJECT
-- =========================================

-- =========================
-- BASIC QUERIES
-- =========================

-- Show all customers
SELECT * FROM customers;

-- Show only first name and country
SELECT first_name, country FROM customers;

-- Find customers from UK
SELECT * FROM customers WHERE country = 'UK';

-- Show orders where amount > 500
SELECT * FROM orders WHERE amount > 500;

-- Show unique items
SELECT DISTINCT item FROM orders;

-- Count total customers
SELECT COUNT(*) AS total_customers FROM customers;

-- Count total orders
SELECT COUNT(*) AS total_orders FROM orders;

-- Max order amount
SELECT MAX(amount) AS max_amount FROM orders;

-- Min order amount
SELECT MIN(amount) AS min_amount FROM orders;

-- Avg order amount
SELECT AVG(amount) AS avg_amount FROM orders;


-- =========================
-- JOIN ANALYSIS
-- =========================

-- Customers with orders
SELECT c.first_name, c.last_name, o.item
FROM customers c
INNER JOIN orders o
ON c.customer_id = o.customer_id;

-- Customers who placed at least one order
SELECT DISTINCT c.customer_id, c.first_name, c.last_name
FROM customers c
INNER JOIN orders o
ON c.customer_id = o.customer_id;

-- Customers with no orders
SELECT c.*
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.customer_id IS NULL;

-- Orders with customer country
SELECT o.*, c.country
FROM orders o
LEFT JOIN customers c
ON o.customer_id = c.customer_id;

-- Customers with shipping status
SELECT c.*, s.status
FROM customers c
LEFT JOIN shippings s
ON c.customer_id = s.customer;


-- =========================
-- BUSINESS AGGREGATIONS
-- =========================

-- Total spending per customer
SELECT c.customer_id, SUM(o.amount) AS total_spent
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id;

-- Number of orders per customer
SELECT c.customer_id, COUNT(o.order_id) AS total_orders
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id;

-- Total sales per country
SELECT c.country, SUM(o.amount) AS total_sales
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.country;

-- Average order value per customer
SELECT c.customer_id, AVG(o.amount) AS avg_order_value
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id;

-- Count customers per country
SELECT country, COUNT(customer_id) AS total_customers
FROM customers
GROUP BY country;

-- Total orders per item
SELECT item, COUNT(order_id) AS total_orders
FROM orders
GROUP BY item;


-- =========================
-- TOP / BUSINESS INSIGHTS
-- =========================

-- Top 2 customers by spending
SELECT TOP 2 c.customer_id, c.first_name,
SUM(o.amount) AS total_spent
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.first_name
ORDER BY total_spent DESC;

-- Top-selling product
SELECT TOP 1 item, SUM(amount) AS revenue
FROM orders
GROUP BY item
ORDER BY revenue DESC;

-- Least-selling product
SELECT TOP 1 item, SUM(amount) AS revenue
FROM orders
GROUP BY item
ORDER BY revenue ASC;

-- Country generating highest revenue
SELECT TOP 1 c.country, SUM(o.amount) AS revenue
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.country
ORDER BY revenue DESC;

-- Customer with highest orders
SELECT TOP 1 c.customer_id, c.first_name,
COUNT(o.order_id) AS order_count
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.first_name
ORDER BY order_count DESC;


-- =========================
-- ADVANCED ANALYSIS
-- =========================

-- Customers who ordered Keyboard
SELECT c.customer_id, c.first_name, o.item
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.item = 'Keyboard';

-- Repeat customers
SELECT c.customer_id, COUNT(o.order_id) AS total_orders
FROM customers c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id
HAVING COUNT(o.order_id) > 1;

-- Customers with multiple different items
SELECT c.customer_id, COUNT(DISTINCT o.item) AS unique_items
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id
HAVING COUNT(DISTINCT o.item) > 1;

-- Customers with no shipping
SELECT c.customer_id, c.first_name
FROM customers c
LEFT JOIN shippings s
ON c.customer_id = s.customer
WHERE s.customer IS NULL;
