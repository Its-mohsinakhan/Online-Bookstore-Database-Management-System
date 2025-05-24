# 📚 Online Bookstore Database Management System

This project is a structured SQL-based database system developed to simulate an **Online Bookstore**. It allows efficient management of books, customers, and orders, and includes advanced querying to derive insights for sales and customer behavior.

## 🧾 Project Overview

The system manages:
- Book listings with genres, prices, and stock levels.
- Customer information and order records.
- Querying and reporting to answer real-world business questions.

---

## 📁 Database Schema

### 🧩 Tables:
1. **Books**
   - `book_id` (Primary Key)
   - `title`
   - `author`
   - `genre`
   - `price`
   - `stock_quantity`

2. **Customers**
   - `customer_id` (Primary Key)
   - `name`
   - `email`
   - `phone`
   - `address`

3. **Orders**
   - `order_id` (Primary Key)
   - `customer_id` (Foreign Key → Customers)
   - `book_id` (Foreign Key → Books)
   - `order_date`
   - `quantity`
   - `total_amount`

---

## 💻 Technologies Used
- **SQL** – Core language for database design and query
- **MySQL / PostgreSQL / SQLite** *(based on your setup)*
- **DB Browser / MySQL Workbench / pgAdmin** *(optional, for GUI-based interaction)*

---

## 🧠 Sample Business Questions Solved

✔️ What are the top 5 best-selling books?  
✔️ How much revenue was generated each month?  
✔️ Which customer has placed the most orders or spent the most?  
✔️ What is the current stock status of each book?  
✔️ Which genres are the most popular?  
✔️ What is the order history of a particular customer?

---

## 📌 Sample SQL Queries

```sql
-- Top 5 best-selling books
SELECT b.title, SUM(o.quantity) AS total_sold
FROM Orders o
JOIN Books b ON o.book_id = b.book_id
GROUP BY b.title
ORDER BY total_sold DESC
LIMIT 5;

-- Monthly revenue report
SELECT DATE_FORMAT(order_date, '%Y-%m') AS month, SUM(total_amount) AS revenue
FROM Orders
GROUP BY month
ORDER BY month;

-- Customer with highest spend
SELECT c.name, SUM(o.total_amount) AS total_spent
FROM Customers c
JOIN Orders o ON c.customer_id = o.customer_id
GROUP BY c.name
ORDER BY total_spent DESC
LIMIT 1;
