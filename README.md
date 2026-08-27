# Product Management System — MySQL

## 📌 Project Overview

The **Product Management System** is a relational database project developed using **MySQL** to manage products, categories, suppliers, customers, orders, and order items.

The project demonstrates practical SQL and database concepts such as:

* Database and table creation
* Primary and foreign keys
* Unique and check constraints
* Data insertion and manipulation
* CRUD operations
* Filtering and sorting
* Aggregate functions
* GROUP BY and HAVING
* INNER JOIN, LEFT JOIN and RIGHT JOIN
* UNION
* CASE statements
* NULL handling with COALESCE
* Subqueries
* Transactions
* COMMIT, ROLLBACK and SAVEPOINT
* Business-oriented SQL reports

The database is designed to represent a basic **e-commerce/product management system**.

---

## 🛠️ Technologies Used

| Technology      | Purpose                                    |
| --------------- | ------------------------------------------ |
| MySQL           | Relational database management             |
| SQL             | Database queries and data manipulation     |
| MySQL Workbench | Query execution and database visualization |

---

## 🗂️ Database Structure

The database is named:

```sql
product_management
```

It contains the following main tables:

1. `categories`
2. `suppliers`
3. `products`
4. `customers`
5. `orders`
6. `order_items`

The SQL script creates the database and defines the required relationships and constraints.

---

## 🏗️ Database Tables

### 1. Categories

Stores product category information.

**Important columns:**

* `category_id` — Primary Key
* `category_name` — Unique category name
* `description` — Category description

---

### 2. Suppliers

Stores supplier information.

**Important columns:**

* `supplier_id` — Primary Key
* `supplier_name`
* `email` — Unique email
* `phone`
* `city`

The project includes supplier data such as ABC Electronics, Tech World, Digital India, Global Electronics and Smart Solutions.

---

### 3. Products

Stores product catalog information.

**Important columns:**

* `product_id` — Primary Key
* `product_name`
* `category_id` — Foreign Key
* `supplier_id` — Foreign Key
* `price`
* `stock_quantity`
* `discount`
* `product_code` — Unique
* `status`
* `created_date`

The table also applies validation rules such as positive prices, non-negative stock, discount between 0 and 100, and predefined product statuses.

---

### 4. Customers

Stores customer details.

**Important columns:**

* `customer_id` — Primary Key
* `customer_name`
* `email` — Unique
* `phone`
* `city`

---

### 5. Orders

Stores customer order information.

**Important columns:**

* `order_id` — Primary Key
* `customer_id` — Foreign Key
* `order_date`
* `order_status`

Supported order statuses include:

* `PLACED`
* `PROCESSING`
* `SHIPPED`
* `DELIVERED`
* `CANCELLED`

---

### 6. Order Items

Stores products associated with individual orders.

**Important columns:**

* `order_item_id` — Primary Key
* `order_id` — Foreign Key
* `product_id` — Foreign Key
* `quantity`
* `unit_price`

The database uses foreign-key relationships to connect order items with orders and products.

---

## 🔗 Database Relationships

The database follows a relational structure:

```text
Categories
     │
     │ 1
     │
     └──────────< Products >────────── Suppliers
                    │
                    │
                    │
                 Order Items
                    │
                    │
                  Orders
                    │
                    │
                Customers
```

### Relationships

* One category can have multiple products.
* One supplier can supply multiple products.
* One customer can place multiple orders.
* One order can contain multiple order items.
* One product can appear in multiple order items.

---

## 📊 Sample Data

The project contains sample e-commerce data including:

### Products

* iPhone 15
* Samsung Galaxy S25
* Dell Inspiron
* HP Pavilion
* Wireless Mouse
* Mechanical Keyboard
* LG Refrigerator
* Sony TV

### Categories

* Electronics
* Mobiles
* Laptops
* Accessories
* Home Appliances

### Customers

* Rahul Sharma
* Priya Das
* Amit Roy
* Sneha Singh
* Arjun Kumar

Sample products, customers and orders are populated in the SQL script.

---

# 🔍 SQL Concepts Implemented

## 1. Database Creation

```sql
DROP DATABASE IF EXISTS product_management;
CREATE DATABASE IF NOT EXISTS product_management;
USE product_management;
```

---

## 2. CRUD Operations

The project demonstrates:

### CREATE

Creating databases and tables.

### READ

```sql
SELECT * FROM products;
```

### UPDATE

```sql
UPDATE products
SET price = price + 1000
WHERE product_id = 5;
```

### DELETE

```sql
DELETE FROM products
WHERE product_id = 7;
```

CRUD operations are demonstrated throughout the SQL script.

---

## 3. Filtering

Examples include:

```sql
WHERE price > 50000
```

```sql
WHERE price BETWEEN 30000 AND 80000
```

```sql
WHERE category_id IN (2, 3)
```

```sql
WHERE product_name LIKE 'S%'
```

The project uses `WHERE`, `AND`, `OR`, `NOT`, `BETWEEN`, `IN`, and `LIKE` for filtering data.

---

## 4. Sorting and Limiting

```sql
ORDER BY price DESC;
```

```sql
ORDER BY price DESC
LIMIT 3;
```

These queries are used to identify products according to price and other criteria.

---

## 5. Aggregate Functions

The project demonstrates:

* `COUNT()`
* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`

Example:

```sql
SELECT AVG(price) AS average_price
FROM products;
```

---

## 6. GROUP BY and HAVING

Example:

```sql
SELECT
    category_id,
    COUNT(*) AS product_count
FROM products
GROUP BY category_id;
```

The project also uses `HAVING` to filter aggregated results.

---

## 7. SQL Joins

The project demonstrates:

### INNER JOIN

Used to combine products with categories and suppliers.

### LEFT JOIN

Used to identify categories even when they have no products.

### RIGHT JOIN

Used to demonstrate reverse-side table matching.

### UNION

Used to combine results from multiple queries.

---

## 8. Order and Customer Analysis

The project combines:

```text
Customers
     ↓
Orders
     ↓
Order Items
     ↓
Products
```

This allows analysis of:

* Customer orders
* Products purchased
* Quantity purchased
* Unit price
* Total order amount
* Customer total spending

---

## 9. CASE Statements

The project uses `CASE` to categorize products.

### Price Category

```text
Price >= 70000     → Premium
Price >= 30000     → Medium
Otherwise          → Budget
```

### Stock Status

```text
0       → Out of Stock
1–10    → Low Stock
11–50   → Normal Stock
>50     → High Stock
```

### Discount Category

Products are also categorized based on their discount percentage.

---

## 10. NULL Handling

The project demonstrates `IS NULL`, `IS NOT NULL`, and `COALESCE()`.

Example:

```sql
SELECT
    product_name,
    COALESCE(discount, 0) AS discount
FROM products;
```

This ensures that a NULL discount can be displayed as `0`.

---

## 11. Subqueries

The project includes subqueries to find:

* Products priced above the average price
* The most expensive product
* Products more expensive than Dell Inspiron

Example:

```sql
SELECT product_name, price
FROM products
WHERE price >
(
    SELECT AVG(price)
    FROM products
);
```

---

# 🔄 Transaction Management

The project demonstrates MySQL transaction concepts.

### COMMIT

```sql
START TRANSACTION;

UPDATE products
SET stock_quantity = stock_quantity - 2
WHERE product_id = 1;

COMMIT;
```

### ROLLBACK

```sql
START TRANSACTION;

UPDATE products
SET stock_quantity = stock_quantity - 5
WHERE product_id = 1;

ROLLBACK;
```

### SAVEPOINT

```sql
START TRANSACTION;

UPDATE products
SET price = price + 500
WHERE product_id = 1;

SAVEPOINT price_update;

UPDATE products
SET stock_quantity = stock_quantity - 5
WHERE product_id = 1;

ROLLBACK TO price_update;

COMMIT;
```

These operations demonstrate how database changes can be committed, reverted, or partially rolled back.

---

# 📈 Business Reports

The project contains several business-oriented reports.

## Report 1 — Product Catalog

Displays:

* Product
* Category
* Supplier
* Price
* Stock
* Discount
* Status

---

## Report 2 — Low Stock Products

Identifies products with stock quantity less than or equal to 10 and classifies them as:

* OUT OF STOCK
* LOW STOCK
* AVAILABLE

---

## Report 3 — Products by Category

Calculates the total number of products in each category.

---

## Report 4 — Order Details

Displays:

* Order ID
* Customer
* Order date
* Product
* Quantity
* Unit price
* Total amount

---

## Report 5 — Product Sales and Revenue

Calculates:

* Units sold
* Revenue
* Product-wise sales performance

Cancelled orders are excluded from the revenue calculation.

---

## Report 6 — Customer Spending

Calculates:

* Total orders
* Total amount spent
* Customer-wise ranking by spending

---

## Report 7 — Order Status Summary

Shows the number of orders for each order status.

```text
PLACED
PROCESSING
SHIPPED
DELIVERED
CANCELLED
```

---

## Report 8 — Product Status Summary

Calculates the number of:

* Active products
* Inactive products
* Discontinued products

---

## Report 9 — Product Price Analysis

Products are divided into:

* Premium
* Medium
* Budget

based on their price.

---

## Report 10 — Product Performance Analysis

The final analysis combines product, category, supplier and order information to calculate:

* Final selling price
* Stock status
* Number of times ordered
* Units sold
* Total revenue

The results are sorted by total revenue.

---

# ⚙️ How to Execute the Project

## Prerequisites

Install:

* MySQL Server
* MySQL Workbench

---

## Step 1 — Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

```bash
cd <YOUR_REPOSITORY_NAME>
```

---

## Step 2 — Open MySQL Workbench

Open **MySQL Workbench** and connect to your local MySQL server.

---

## Step 3 — Open the SQL File

Open:

```text
product_management.sql
```

---

## Step 4 — Execute the SQL Script

Run the complete SQL script.

The script will:

1. Create the `product_management` database.
2. Create all required tables.
3. Add constraints and relationships.
4. Insert sample data.
5. Execute SQL queries.
6. Demonstrate joins and aggregations.
7. Demonstrate transactions.
8. Generate business reports.

---

## Step 5 — Verify Database

Run:

```sql
USE product_management;

SHOW TABLES;
```

You should see:

```text
categories
suppliers
products
customers
orders
order_items
```

---

# 📸 Execution & Output Screenshots

The following screenshots demonstrate the successful execution of the project in **MySQL Shell**.

<img width="1902" height="921" alt="Output_image1" src="https://github.com/user-attachments/assets/159ad35c-d63b-4364-9166-cacf7808cc4e" />
<img width="1912" height="921" alt="Output_image2" src="https://github.com/user-attachments/assets/2e43a0ab-47e1-4874-bc50-2a106bba34ab" />
<img width="1911" height="790" alt="Output_image3" src="https://github.com/user-attachments/assets/cd5934e0-2b0e-40d6-ae2c-baa91ff5a467" />
<img width="1912" height="947" alt="Output_image4" src="https://github.com/user-attachments/assets/f25d2c75-78f9-44db-905c-14671ea669ca" />
<img width="1912" height="823" alt="Output_image5" src="https://github.com/user-attachments/assets/15a98ae1-6446-466e-91e1-56768c961105" />
<img width="1917" height="837" alt="Output_image6" src="https://github.com/user-attachments/assets/9d52c798-3ddb-4345-800d-df7e0eeb39fa" />
<img width="1915" height="842" alt="Output_image7" src="https://github.com/user-attachments/assets/aabaf978-2be9-468f-8a5f-64b9a4fcebb8" />
<img width="1912" height="882" alt="Output_image8" src="https://github.com/user-attachments/assets/463363f3-11e4-42f0-b562-62fab7f3c7d1" />
<img width="1915" height="796" alt="Output_image9" src="https://github.com/user-attachments/assets/40b7843c-bfa4-4c94-b533-2188c956d08b" />
<img width="1917" height="960" alt="Output_image10" src="https://github.com/user-attachments/assets/dd444413-b7f3-4e4a-add3-37d27f0baf40" />
<img width="1917" height="842" alt="Output_image11" src="https://github.com/user-attachments/assets/7693fea7-0137-4d38-9af2-d44baf8dda8b" />
<img width="1912" height="905" alt="Output_image12" src="https://github.com/user-attachments/assets/c8f8f26a-1018-4b31-8563-5438620038a5" />
<img width="1912" height="760" alt="Output_image13" src="https://github.com/user-attachments/assets/1546bcd1-fdbc-4f6d-b4c1-8f22a7e73be7" />
<img width="1917" height="950" alt="Output_image14" src="https://github.com/user-attachments/assets/f2ef367f-c70f-4bc1-8fc9-6b2ffe28fd97" />
<img width="1910" height="956" alt="Output_image15" src="https://github.com/user-attachments/assets/5bc614e7-e9ca-4645-ae22-610950b0a14e" />
<img width="1910" height="941" alt="Output_image16" src="https://github.com/user-attachments/assets/94824d3f-f16d-4651-b5f9-963b059d69ef" />
<img width="1917" height="948" alt="Output_image17" src="https://github.com/user-attachments/assets/d662d1a7-07f7-4131-8429-3de321e9428e" />
<img width="1913" height="932" alt="Output_image18" src="https://github.com/user-attachments/assets/3e9fbef1-8ffa-4451-b39e-8bd1d4b1b08a" />
<img width="1917" height="963" alt="Output_image19" src="https://github.com/user-attachments/assets/1d467c46-d2fc-40f9-92ca-9a8e477c7374" />
<img width="1917" height="818" alt="Output_image20" src="https://github.com/user-attachments/assets/47b23d48-c91a-43c8-b0c1-2e4fa2921980" />
<img width="1916" height="918" alt="Output_image21" src="https://github.com/user-attachments/assets/3abf0800-173c-40ae-bb2e-4676cb1090b5" />
<img width="1917" height="922" alt="Output_image22" src="https://github.com/user-attachments/assets/dcb3d0bc-8109-479a-bfe4-78d7cc22ce74" />
<img width="1915" height="821" alt="Output_image23" src="https://github.com/user-attachments/assets/caa97b19-081a-4626-a00b-44f9f9ec367b" />
<img width="1917" height="873" alt="Output_image24" src="https://github.com/user-attachments/assets/b2bc4fea-d194-4ffc-b92d-dbca4c0ac81b" />


---

# 🎯 Key Learning Outcomes

Through this project, I gained practical experience in:

* Designing relational databases
* Creating normalized database tables
* Implementing primary and foreign keys
* Applying database constraints
* Writing SQL queries
* Performing CRUD operations
* Filtering and sorting records
* Using aggregate functions
* Working with joins
* Writing subqueries
* Handling NULL values
* Using conditional logic with CASE
* Managing transactions
* Generating business reports
* Performing product, customer and sales analysis

---

# 💼 Project Highlights

### Database Design

Designed a relational product management database with **6 interconnected tables**.

### Data Management

Implemented product, supplier, customer and order management using SQL.

### Data Analysis

Created queries to analyze product prices, stock levels, customer spending, order status and revenue.

### Advanced SQL

Implemented joins, subqueries, CASE statements, aggregate functions and NULL handling.

### Transaction Management

Demonstrated `COMMIT`, `ROLLBACK` and `SAVEPOINT` for maintaining data consistency.

### Business Reporting

Created multiple reports for product catalog, inventory, orders, sales, revenue and customer spending.

---

# 🚀 Future Enhancements

Possible future improvements include:

* Creating a web-based frontend
* Adding user authentication
* Building an admin dashboard
* Connecting the database with Python/Flask
* Adding stored procedures
* Adding triggers for automatic stock updates
* Implementing indexes for query optimization
* Adding more advanced sales analytics
* Creating Power BI/Tableau dashboards
* Deploying the database-backed application to the cloud

---

# 👩‍💻 Author

**Shreyasree Mete**

---

## ⭐ Project Summary

This project demonstrates the practical use of **MySQL and SQL for designing and managing an e-commerce-style product management system**, from database creation and data manipulation to advanced analysis, transaction management and business reporting.
