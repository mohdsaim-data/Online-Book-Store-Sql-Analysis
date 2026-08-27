# 📚 Online Book Store Data Analysis using SQL

![SQL](https://img.shields.io/badge/SQL-PostgreSQL-blue)
![Database](https://img.shields.io/badge/Database-PostgreSQL-336791)
![Project](https://img.shields.io/badge/Project-Data%20Analysis-green)

## 📌 Project Overview

This project focuses on analyzing an **Online Book Store database using SQL and PostgreSQL**.

The project uses three related datasets:

- 📚 Books
- 👥 Customers
- 🛒 Orders

The purpose of this project is to use SQL to extract useful business insights related to **books, customers, sales, revenue, genres, pricing, and inventory**.

---

## 🎯 Project Objectives

The main objectives of this project are:

1. Retrieve books based on genre.
2. Find books published after a specific year.
3. Identify customers from a specific country.
4. Analyze orders placed during a specific month.
5. Calculate total available book stock.
6. Find the most expensive book.
7. Identify orders containing more than one book.
8. Find orders above a specific amount.
9. Identify all available book genres.
10. Find the book with the lowest stock.
11. Calculate total revenue.
12. Calculate books sold by genre.
13. Find the average price of Fantasy books.
14. Identify customers who placed at least two orders.
15. Find the most frequently ordered book.
16. Find the top 3 most expensive Fantasy books.
17. Calculate books sold by each author.
18. Identify cities of customers who spent more than $30 on an order.
19. Find the customer who spent the most.
20. Calculate remaining stock after fulfilling orders.

---

## 🛠️ Tools & Technologies

- **PostgreSQL**
- **SQL**
- **pgAdmin**
- **CSV**
- **GitHub**

---

# 📂 Dataset Description

The project contains three datasets.

## 📚 Books Dataset

The `Books` table contains **500 records** and **7 columns**.

| Column | Description |
|---|---|
| `Book_ID` | Unique ID of the book |
| `Title` | Title of the book |
| `Author` | Author of the book |
| `Genre` | Genre/category of the book |
| `Published_Year` | Year the book was published |
| `Price` | Price of the book |
| `Stock` | Available stock |

## 👥 Customers Dataset

The `Customers` table contains **500 records** and **6 columns**.

| Column | Description |
|---|---|
| `Customer_ID` | Unique customer ID |
| `Name` | Customer name |
| `Email` | Customer email |
| `Phone` | Customer phone number |
| `City` | Customer city |
| `Country` | Customer country |

## 🛒 Orders Dataset

The `Orders` table contains **500 records** and **6 columns**.

| Column | Description |
|---|---|
| `Order_ID` | Unique order ID |
| `Customer_ID` | Customer who placed the order |
| `Book_ID` | Book that was ordered |
| `Order_Date` | Date of the order |
| `Quantity` | Number of books ordered |
| `Total_Amount` | Total value of the order |

---

# 🗄️ Database Setup

## Create Books Table

```sql
CREATE TABLE Books (
    Book_ID SERIAL PRIMARY KEY,
    Title VARCHAR(100),
    Author VARCHAR(100),
    Genre VARCHAR(50),
    Published_Year INT,
    Price NUMERIC(10, 2),
    Stock INT
);
```

## Create Customers Table

```sql
CREATE TABLE Customers (
    Customer_ID SERIAL PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100),
    Phone VARCHAR(15),
    City VARCHAR(50),
    Country VARCHAR(150)
);
```

## Create Orders Table

```sql
CREATE TABLE Orders (
    Order_ID SERIAL PRIMARY KEY,
    Customer_ID INT REFERENCES Customers(Customer_ID),
    Book_ID INT REFERENCES Books(Book_ID),
    Order_Date DATE,
    Quantity INT,
    Total_Amount NUMERIC(10, 2)
);
```

---

# 📊 SQL Analysis & Questions

# 🔹 Basic SQL Questions

## 1️⃣ Retrieve all books in the "Fiction" genre

### SQL Query

```sql
SELECT *
FROM Books
WHERE Genre = 'Fiction';
```

### Formula / Logic

```text
Filter records where Genre = 'Fiction'
```

### Result

**60 Fiction books** were found.

### Insight

The dataset contains **60 books in the Fiction genre**.

---

## 2️⃣ Find books published after the year 1950

### SQL Query

```sql
SELECT *
FROM Books
WHERE Published_Year > 1950;
```

### Formula / Logic

```text
Published Year > 1950
```

### Result

**292 books** were published after 1950.

### Insight

More than half of the books in the dataset were published after 1950.

---

## 3️⃣ List all customers from Canada

### SQL Query

```sql
SELECT *
FROM Customers
WHERE Country = 'Canada';
```

### Formula / Logic

```text
Country = 'Canada'
```

### Result

**3 customers** are from Canada.

---

## 4️⃣ Show orders placed in November 2023

### SQL Query

```sql
SELECT *
FROM Orders
WHERE Order_Date BETWEEN '2023-11-01' AND '2023-11-30';
```

### Formula / Logic

```text
Order Date BETWEEN
01-Nov-2023 AND 30-Nov-2023
```

### Result

- **25 orders**
- **118 books ordered**
- **$3,291.56 total order value**

### Insight

There were **25 orders** placed during November 2023.

---

## 5️⃣ Retrieve the total stock of books available

### SQL Query

```sql
SELECT
    SUM(Stock) AS Total_Stock
FROM Books;
```

### Formula

```text
Total Stock = SUM(Stock)
```

### Result

**25,056 books**

### Insight

The bookstore has a total listed inventory of **25,056 books**.

---

## 6️⃣ Find the details of the most expensive book

### SQL Query

```sql
SELECT *
FROM Books
ORDER BY Price DESC
LIMIT 1;
```

### Formula / Logic

```text
Maximum Price = MAX(Price)
```

### Result

| Attribute | Value |
|---|---|
| Book ID | 340 |
| Title | Proactive system-worthy orchestration |
| Author | Robert Scott |
| Genre | Mystery |
| Published Year | 1907 |
| Price | $49.98 |
| Stock | 88 |

### Insight

The most expensive book in the dataset costs **$49.98**.

---

## 7️⃣ Show all customers who ordered more than 1 quantity of a book

### SQL Query

```sql
SELECT *
FROM Orders
WHERE Quantity > 1;
```

### Formula / Logic

```text
Quantity > 1
```

### Result

**438 orders** contain more than one book.

### Insight

The majority of orders in the dataset contain multiple copies of a book.

---

## 8️⃣ Retrieve all orders where the total amount exceeds $20

### SQL Query

```sql
SELECT *
FROM Orders
WHERE Total_Amount > 20;
```

### Formula / Logic

```text
Total Amount > $20
```

### Result

**473 orders** have a total value greater than $20.

---

## 9️⃣ List all genres available in the Books table

### SQL Query

```sql
SELECT DISTINCT Genre
FROM Books;
```

### Result

The dataset contains **7 genres**:

1. Biography
2. Fantasy
3. Fiction
4. Mystery
5. Non-Fiction
6. Romance
7. Science Fiction

### Insight

The bookstore offers books across **7 different genres**.

---

## 🔟 Find the book with the lowest stock

### SQL Query

```sql
SELECT *
FROM Books
ORDER BY Stock
LIMIT 1;
```

### Formula / Logic

```text
Minimum Stock = MIN(Stock)
```

### Result

| Attribute | Value |
|---|---|
| Book ID | 44 |
| Title | Networked systemic implementation |
| Author | Ryan Frank |
| Genre | Science Fiction |
| Published Year | 1965 |
| Price | $13.55 |
| Stock | 0 |

### Insight

The book **Networked systemic implementation** currently has **0 units of stock**.

---

## 1️⃣1️⃣ Calculate the total revenue generated from all orders

### SQL Query

```sql
SELECT
    SUM(Total_Amount) AS Revenue
FROM Orders;
```

### Formula

```text
Total Revenue = SUM(Total_Amount)
```

### Result

**$75,628.66**

### Insight

The 500 orders generated a total recorded revenue of **$75,628.66**.

---

# 🔥 Advanced SQL Questions

## 1️⃣ Retrieve the total number of books sold for each genre

### SQL Query

```sql
SELECT
    b.Genre,
    SUM(o.Quantity) AS Total_Books_Sold
FROM Orders o
JOIN Books b
    ON o.Book_ID = b.Book_ID
GROUP BY b.Genre;
```

### Formula

```text
Books Sold per Genre =
SUM(Order Quantity)
GROUP BY Genre
```

### Result

| Genre | Books Sold |
|---|---:|
| Mystery | 504 |
| Science Fiction | 447 |
| Fantasy | 446 |
| Romance | 439 |
| Non-Fiction | 351 |
| Biography | 285 |
| Fiction | 225 |

### Insight

**Mystery** is the best-selling genre with **504 books sold**.

---

## 2️⃣ Find the average price of books in the "Fantasy" genre

### SQL Query

```sql
SELECT
    AVG(Price) AS Average_Price
FROM Books
WHERE Genre = 'Fantasy';
```

### Formula

```text
Average Price =
SUM(Fantasy Book Prices) /
Number of Fantasy Books
```

### Result

**$25.98**

### Insight

The average price of a Fantasy book is approximately **$25.98**.

---

## 3️⃣ List customers who have placed at least 2 orders

### SQL Query

```sql
SELECT
    o.Customer_ID,
    c.Name,
    COUNT(o.Order_ID) AS Order_Count
FROM Orders o
JOIN Customers c
    ON o.Customer_ID = c.Customer_ID
GROUP BY o.Customer_ID, c.Name
HAVING COUNT(o.Order_ID) >= 2;
```

### Formula / Logic

```text
Order Count = COUNT(Order_ID)

Filter:
Order Count >= 2
```

### Result

**139 customers** placed at least 2 orders.

### Insight

139 customers are repeat customers based on the order count in this dataset.

---

## 4️⃣ Find the most frequently ordered book

### SQL Query

```sql
SELECT
    o.Book_ID,
    b.Title,
    COUNT(o.Order_ID) AS Order_Count
FROM Orders o
JOIN Books b
    ON o.Book_ID = b.Book_ID
GROUP BY o.Book_ID, b.Title
ORDER BY Order_Count DESC
LIMIT 1;
```

### Formula

```text
Order Frequency = COUNT(Order_ID)
```

### Result

The highest order frequency is **4 orders**.

There are multiple books tied at 4 orders, including:

| Book ID | Title | Orders |
|---:|---|---:|
| 31 | Implemented encompassing conglomeration | 4 |
| 120 | Integrated secondary access | 4 |
| 273 | Devolved zero administration process improvement | 4 |
| 333 | Advanced responsive extranet | 4 |
| 491 | Pre-emptive intangible adapter | 4 |

### Insight

The highest order frequency for a single book is **4 orders**.

> **Note:** The original SQL uses `LIMIT 1`, so PostgreSQL may return any one of the tied books unless an additional tie-breaking `ORDER BY` is added.

---

## 5️⃣ Show the top 3 most expensive books of the Fantasy genre

### SQL Query

```sql
SELECT *
FROM Books
WHERE Genre = 'Fantasy'
ORDER BY Price DESC
LIMIT 3;
```

### Formula / Logic

```text
Filter:
Genre = 'Fantasy'

Sort:
Price DESC

Return:
Top 3
```

### Result

| Rank | Book ID | Title | Price |
|---:|---:|---|---:|
| 1 | 240 | Stand-alone content-based hub | $49.90 |
| 2 | 462 | Innovative 3rdgeneration database | $49.23 |
| 3 | 238 | Optimized even-keeled analyzer | $48.97 |

### Insight

The most expensive Fantasy book costs **$49.90**.

---

## 6️⃣ Retrieve the total quantity of books sold by each author

### SQL Query

```sql
SELECT
    b.Author,
    SUM(o.Quantity) AS Total_Books_Sold
FROM Orders o
JOIN Books b
    ON o.Book_ID = b.Book_ID
GROUP BY b.Author;
```

### Formula

```text
Books Sold per Author =
SUM(Order Quantity)
GROUP BY Author
```

### Top Result

| Author | Books Sold |
|---|---:|
| Patrick Contreras | 28 |
| Melissa Taylor | 27 |
| Emily James | 24 |
| Thomas Trujillo | 24 |
| Valerie Moore | 23 |

### Insight

**Patrick Contreras** has the highest total quantity sold with **28 books**.

---

## 7️⃣ List the cities where customers who spent over $30 are located

### SQL Query

```sql
SELECT DISTINCT
    c.City,
    o.Total_Amount
FROM Orders o
JOIN Customers c
    ON o.Customer_ID = c.Customer_ID
WHERE o.Total_Amount > 30;
```

### Formula / Logic

```text
Filter orders where:
Total Amount > $30

Then retrieve:
Customer City
```

### Result

The query identifies the cities of customers whose individual order value exceeded **$30**.

Examples include:

- Lake Paul
- North Keith
- Kelseyfort
- East David
- Ravenberg
- Thomaschester
- Smithmouth
- Bakerton
- South Rachelview
- East Richardburgh
- Many others

### Insight

Customers from many different cities placed orders worth more than **$30**, showing that higher-value orders are geographically distributed across the customer base.

> **Note:** Because the original query selects `DISTINCT City, Total_Amount`, the same city can appear more than once when different orders have different amounts.

---

## 8️⃣ Find the customer who spent the most on orders

### SQL Query

```sql
SELECT
    c.Customer_ID,
    c.Name,
    SUM(o.Total_Amount) AS Total_Spent
FROM Orders o
JOIN Customers c
    ON o.Customer_ID = c.Customer_ID
GROUP BY c.Customer_ID, c.Name
ORDER BY Total_Spent DESC
LIMIT 1;
```

### Formula

```text
Total Customer Spending =
SUM(Total_Amount)
GROUP BY Customer
```

### Result

| Attribute | Value |
|---|---|
| Customer ID | 457 |
| Customer | Kim Turner |
| Total Spent | $1,398.90 |
| City | South Rachelview |
| Country | Cambodia |

### Insight

**Kim Turner** is the highest-spending customer with total purchases of **$1,398.90**.

---

## 9️⃣ Calculate the stock remaining after fulfilling all orders

### SQL Query

```sql
SELECT
    b.Book_ID,
    b.Title,
    b.Stock,
    COALESCE(SUM(o.Quantity), 0) AS Order_Quantity,
    b.Stock - COALESCE(SUM(o.Quantity), 0) AS Remaining_Quantity
FROM Books b
LEFT JOIN Orders o
    ON b.Book_ID = o.Book_ID
GROUP BY b.Book_ID
ORDER BY b.Book_ID;
```

### Formula

```text
Remaining Stock =
Original Stock - Total Ordered Quantity
```

### Result

The analysis shows:

- **30 books** have negative remaining stock.
- **6 books** have exactly 0 remaining stock.
- The lowest calculated remaining stock is **-18 units**.

### Example

| Book ID | Title | Stock | Ordered | Remaining |
|---:|---|---:|---:|---:|
| 491 | Pre-emptive intangible adapter | 2 | 20 | -18 |
| 307 | Expanded local infrastructure | 7 | 23 | -16 |
| 323 | Balanced dynamic project | 2 | 16 | -14 |
| 288 | Re-contextualized real-time Graphic Interface | 9 | 23 | -14 |
| 110 | Re-contextualized radical matrix | 2 | 15 | -13 |

### Insight

Negative remaining stock indicates potential **inventory shortages or overselling** if the listed stock represents the starting inventory.

---

# 🧮 Important SQL Formulas Used

| Requirement | SQL Function / Logic |
|---|---|
| Total | `SUM(column)` |
| Average | `AVG(column)` |
| Maximum | `MAX(column)` |
| Minimum | `MIN(column)` |
| Count | `COUNT(column)` |
| Unique values | `DISTINCT` |
| Filter | `WHERE` |
| Group data | `GROUP BY` |
| Filter grouped results | `HAVING` |
| Sort high to low | `ORDER BY column DESC` |
| Sort low to high | `ORDER BY column ASC` |
| Top N records | `LIMIT N` |
| Combine tables | `JOIN` |
| Preserve unmatched records | `LEFT JOIN` |
| Replace NULL | `COALESCE()` |
| Date range | `BETWEEN` |
| Remaining Stock | `Stock - SUM(Quantity)` |

---

# 🔗 SQL Relationships

The project uses relationships between the three tables.

```text
Customers
    │
    │ Customer_ID
    ▼
Orders
    │
    │ Book_ID
    ▼
Books
```

### Relationship

```text
Customers.Customer_ID
        ↓
Orders.Customer_ID

Books.Book_ID
        ↓
Orders.Book_ID
```

This allows customer information and book information to be combined with order information using SQL `JOIN`.

---

# 💡 Key Business Insights

## 👥 Customer Insights

- Dataset contains **500 customers**.
- **139 customers** placed at least 2 orders.
- **Kim Turner** is the highest-spending customer with **$1,398.90** in purchases.
- Customers from Canada: **3**.

## 📚 Book Insights

- Dataset contains **500 books**.
- Total listed stock: **25,056 books**.
- There are **7 different genres**.
- Most expensive book: **Proactive system-worthy orchestration — $49.98**.
- Lowest-stock book: **Networked systemic implementation — 0 units**.

## 🛒 Sales Insights

- Total orders: **500**.
- Total revenue: **$75,628.66**.
- **438 orders** contain more than one book.
- **473 orders** have a value greater than $20.
- Mystery is the best-selling genre with **504 books sold**.

## 📦 Inventory Insights

- **30 books** have negative calculated remaining stock after fulfilling recorded orders.
- **6 books** have zero calculated remaining stock.
- The lowest calculated remaining stock is **-18 units**.

This could indicate potential **stock management issues, overselling, or that the stock column represents current rather than opening inventory**.

---

# 📈 Business Questions Answered

This project demonstrates how SQL can answer real-world online bookstore questions:

- Which genre has the most books?
- Which books are the most expensive?
- Which books are running out of stock?
- How much revenue does the bookstore generate?
- Which genre sells the most books?
- What is the average price of Fantasy books?
- Which customers are repeat buyers?
- Who is the highest-spending customer?
- Which books are ordered most frequently?
- Which authors sell the most books?
- Where are high-value customers located?
- How much inventory remains after orders?

---

# 🧠 SQL Concepts Demonstrated

```text
SELECT
WHERE
DISTINCT
SUM()
AVG()
MAX()
MIN()
COUNT()
GROUP BY
HAVING
ORDER BY
ASC
DESC
LIMIT
INNER JOIN
LEFT JOIN
COALESCE()
BETWEEN
Aggregate Functions
Date Filtering
Table Relationships
```

---

# 📁 Project Structure

```text
Online-Book-Store-SQL-Analysis/
│
├── Books_Dataset.csv
├── Customers_Dataset.csv
├── Orders_Dataset.csv
├── Online_Books_Store.sql
└── README.md
```

---

# ▶️ How to Run the Project

### 1. Install PostgreSQL

Install PostgreSQL and open **pgAdmin**.

### 2. Create a Database

Create a new PostgreSQL database for the project.

### 3. Create the Tables

Run the table creation queries from:

```text
Online_Books_Store.sql
```

### 4. Import the CSV Files

Import the following datasets into their respective tables:

```text
Books_Dataset.csv
Customers_Dataset.csv
Orders_Dataset.csv
```

### 5. Run the Queries

Open `Online_Books_Store.sql` in the PostgreSQL Query Tool and execute the queries one by one.

---

# 🎓 Skills Demonstrated

Through this project, I demonstrated:

- SQL Query Writing
- PostgreSQL
- Data Analysis
- Data Aggregation
- Filtering & Sorting
- GROUP BY & HAVING
- INNER JOIN
- LEFT JOIN
- Aggregate Functions
- Customer Analysis
- Sales Analysis
- Revenue Analysis
- Inventory Analysis
- Business Insight Generation
- GitHub Documentation

---

# 🚀 Conclusion

This project demonstrates how SQL can be used to transform raw **online bookstore data** into meaningful business insights.

By analyzing books, customers, and orders, the project covers important areas such as:

**Sales → Revenue → Customers → Books → Genres → Pricing → Inventory**

The analysis demonstrates practical SQL skills that can be applied to **Data Analyst, Business Analyst, and SQL Developer** roles.

---

# 👤 Author

**Mohd Saim**

B.Com (Hons.) | Aspiring Data / Business Analyst

### 🔗 GitHub

Add your GitHub profile here:

```text
https://github.com/your-username
```

---

## ⭐ If you found this project useful

Feel free to ⭐ the repository and use the SQL queries for learning and practice.
