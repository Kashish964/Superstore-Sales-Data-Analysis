# Global Superstore – Sales & Profit Analysis (SQL)

A set of SQL queries that analyse the **Global Superstore** dataset to find overall business performance, the best and worst performing categories, top products, and loss-making regions.

---

## Dataset

- **Table name:** `Global_Superstore2`
- **Source:** Global Superstore dataset (retail orders across multiple countries and regions)
- **Key columns used:**

| Column         | Description                              |
|----------------|------------------------------------------|
| `Sales`        | Revenue from each order line             |
| `Profit`       | Profit (or loss) from each order line    |
| `Category`     | Product category (e.g. Technology, Furniture, Office Supplies) |
| `Product_Name` | Name of the product sold                 |
| `Region`       | Sales region                             |

---

## Queries Included

### 1. View the full dataset
```sql
SELECT * FROM Global_Superstore2;
```
Shows all rows and columns, to check the data loaded correctly.

### 2. Overall business performance
```sql
SELECT 
    ROUND(SUM(Sales), 2) AS Total_Revenue,
    ROUND(SUM(Profit), 2) AS Total_Profit,
    ROUND((SUM(Profit) / SUM(Sales)) * 100, 2) AS Profit_Margin_Percent
FROM Global_Superstore2;
```
Returns **total revenue**, **total profit**, and **profit margin %** for the whole business.

### 3. Revenue and profit by category
```sql
SELECT 
    Category,
    ROUND(SUM(Sales), 2) AS Category_Revenue,
    ROUND(SUM(Profit), 2) AS Category_Profit
FROM Global_Superstore2
GROUP BY Category
ORDER BY Category_Profit DESC;
```
Shows which product category earns the most profit (highest first).

### 4. Top 10 most profitable products
```sql
SELECT 
    Product_Name,
    ROUND(SUM(Profit), 2) AS Total_Product_Profit
FROM Global_Superstore2
GROUP BY Product_Name
ORDER BY Total_Product_Profit DESC
LIMIT 10;
```
Lists the 10 products that generate the highest total profit.

### 5. Loss-making regions
```sql
SELECT 
    Region,
    ROUND(SUM(Sales), 2) AS Regional_Sales,
    ROUND(SUM(Profit), 2) AS Regional_Profit
FROM Global_Superstore2
GROUP BY Region
HAVING SUM(Profit) < 0
ORDER BY Regional_Profit ASC;
```
Shows only regions with **negative total profit**, biggest loss first. If no rows are returned, every region is profitable.

---

## SQL Concepts Used

- `SUM()` – total of a column
- `ROUND()` – round results to 2 decimal places
- `GROUP BY` – summarise data by category, product, or region
- `ORDER BY ... DESC / ASC` – sort results
- `HAVING` – filter grouped results (used to find loss-making regions)
- `LIMIT` – return only the top N rows

---

## How to Run

1. Import the Global Superstore dataset into your database (MySQL, PostgreSQL, SQLite, etc.) as a table named `Global_Superstore2`.
2. Make sure column names match those above (e.g. `Product_Name`, not `Product Name`).
3. Open the `.sql` file in your SQL tool (MySQL Workbench, DBeaver, pgAdmin, etc.).
4. Run each query one by one and review the results.

> **Note:** `LIMIT` works in MySQL, PostgreSQL and SQLite. In SQL Server use `SELECT TOP 10 ...` instead.

---

## Key Questions Answered

1. How much revenue and profit did the business make overall?
2. What is the overall profit margin?
3. Which category is the most (and least) profitable?
4. Which products bring in the most profit?
5. Are any regions running at a loss?
