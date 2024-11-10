# SQL Quick Revision

This repository provides a quick revision of essential SQL queries. Use it to brush up on SQL basics and advanced topics quickly.

## Table of Contents
1. [Creating Database and Tables](#creating-database-and-tables)
2. [Inserting Data](#inserting-data)
3. [Querying Data](#querying-data)
4. [Advanced Queries](#advanced-queries)
5. [Updates and Alterations](#updates-and-alterations)

## Creating Database and Tables

CREATE DATABASE sales;
USE sales;

CREATE TABLE orders (
    order_id INT,
    customer_id INT,
    order_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    amount DECIMAL(10,2) NOT NULL,
    PRIMARY KEY (order_id, customer_id)
);

**Inserting Data**
INSERT INTO orders (order_id, customer_id, order_date, amount) VALUES 
(1, 01, '2024-11-10 06:04:10', 150.00),
(2, 02, '2024-04-25 10:30:00', 200.50),
(3, 03, '2024-11-10 06:05:27', 175.75),
(4, 04, '2024-11-10 06:05:27', 220.00),
(5, 05, '2024-11-10 06:05:27', 99.99);

**Querying Data**
SELECT * FROM orders;
SELECT order_id FROM orders WHERE amount = 150.00;
SELECT order_id, customer_id FROM orders WHERE order_id = 1 AND customer_id = 01;
SELECT order_id , COUNT(*) AS id FROM orders GROUP BY order_id;

**Advanced Queries**
SELECT amount , SUM(amount) AS adds FROM orders GROUP BY amount;
SELECT amount , AVG(amount) AS avgs FROM orders GROUP BY amount;
SELECT amount, MIN(amount) AS mins FROM orders GROUP BY amount;
SELECT customer_id, MIN(amount) AS mins FROM orders GROUP BY customer_id;
SELECT date(order_date) AS od, time(order_date) AS ot FROM orders;
ALTER TABLE orders ADD COLUMN order_name VARCHAR(100) NOT NULL DEFAULT 'clothes';

**Updates and Alterations**
UPDATE orders SET order_name = 'cotton' WHERE order_id = 1;
SELECT order_name FROM orders WHERE order_id = 1;
UPDATE orders SET order_name = 'wool', amount = 500.00 WHERE order_id = 2;
SELECT order_name, amount FROM orders WHERE order_id = 2;
SELECT * FROM orders WHERE order_name LIKE 'c%';
SELECT order_id FROM orders WHERE customer_id = 1 UNION SELECT order_id FROM orders WHERE customer_id = 2;
SELECT customer_id, CASE 
    WHEN amount > 1000 THEN 'high' 
    WHEN amount BETWEEN 120.00 AND 150.00 THEN 'medium' 
    ELSE 'low' 
END AS amount_category FROM orders;
