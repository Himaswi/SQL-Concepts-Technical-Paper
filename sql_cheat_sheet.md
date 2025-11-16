 ### A Clear and Detailed Explanation of Fundamental Database Concepts

## 1. Introduction

Databases are essential components of modern applications. SQL (Structured Query Language) enables efficient **storage, retrieval, processing, and management** of data.

To design scalable, consistent, and high-performance systems, it is important to understand concepts like **ACID**, **CAP theorem**, **Joins**, **Transactions**, **Indexes**, and more.

This technical paper explains all essential SQL concepts.

---

## 2. ACID Properties

ACID stands for **Atomicity, Consistency, Isolation, Durability**.

### **2.1 Atomicity**
- A transaction should execute **fully or not at all**.

### **2.2 Consistency**
- A transaction must keep the database in a **valid state** after execution.

### **2.3 Isolation**
- Multiple transactions should not interfere with each other.

### **2.4 Durability**
- Once committed, data should be **permanently stored**.

---

## 3. CAP Theorem

A distributed database can guarantee only **two** of the following three:

### **3.1 Consistency (C)**
- All nodes return the **same, most recent** data.

### **3.2 Availability (A)**
- Every request gets a response, even during failures.

### **3.3 Partition Tolerance (P)**
- System continues working despite **network failures**.

> **You can choose only two: CP, AP, or CA (not possible in distributed systems).**

---

## 4. Joins in SQL

Joins combine rows from two or more tables based on a related column.
### Types of Joins in SQL
- **JOIN** (Default: works as INNER JOIN)
- **INNER JOIN**
- **OUTER JOIN**
  - **LEFT OUTER JOIN (LEFT JOIN)**
  - **RIGHT OUTER JOIN (RIGHT JOIN)**
  - **FULL OUTER JOIN**

### **4.1 INNER JOIN**
- Returns only the rows where there is a match in both tables.
- Rows with no matching values in either table are excluded.
### Code:
```sql
SELECT *
FROM TableA
INNER JOIN TableB ON TableA.id = TableB.id;
```
### 4.2 LEFT JOIN (LEFT OUTER JOIN)
- Returns all rows from the left table and matching rows from the right table.
- If no match exists, NULL values are returned for columns from the right table.

### Code:
```sql
SELECT *
FROM TableA
LEFT JOIN TableB ON TableA.id = TableB.id;
```
### 4.3 RIGHT JOIN (RIGHT OUTER JOIN)
- Returns all rows from the right table and matching rows from the left table.
- If no match exists, NULL values appear for the left table’s columns.

### Code:
```sql
SELECT *
FROM TableA
RIGHT JOIN TableB ON TableA.id = TableB.id;
```
### 4.4 FULL JOIN (FULL OUTER JOIN)
- Returns all rows when there is a match in either the left or the right table.
- Non-matching rows return NULL values for the columns from the opposite table.

### Code:
```sql
SELECT *
FROM TableA
FULL OUTER JOIN TableB ON TableA.id = TableB.id;
```
### 4.5 CROSS JOIN
- Returns the Cartesian product of both tables.
- Every row in TableA is combined with every row in TableB.
- No join condition is required.

### Code:
```sql
SELECT *
FROM TableA
CROSS JOIN TableB;
```
### 4.6 SELF JOIN
- A table joins with itself using aliases.
- Useful for comparing rows within the same table (e.g., employees and managers).

### Code:
```sql
SELECT T1.column_name, T2.column_name
FROM Employees T1, Employees T2
WHERE T1.manager_id = T2.employee_id;
```
## 5 Aggregations and Filters in SQL
### 5.1 Aggregation Functions
Aggregation functions perform calculations on groups of rows and return a single value.

### Common Aggregation Functions:
- **COUNT()** – Returns the number of rows.
- **SUM()** – Returns the total value.
- **AVG()** – Returns the average value.
- **MAX()** – Returns the maximum value.
- **MIN()** – Returns the minimum value.
  ### Example:
```sql
SELECT department, COUNT(*), AVG(salary), MAX(salary), MIN(salary)
FROM employees
GROUP BY department;
```
- **GROUP BY Clause**
  - Used to group rows that have the same values in specified columns.
  - Usually used with aggregation functions.
  ### Example:
```
    SELECT department, COUNT(*)
    FROM employees
    GROUP BY department;
  ```
### 5.2 SQL Filters (Common Filtering Conditions)
# SQL Filters – Table Format

| Filter | Description |
|--------|-------------|
| **WHERE** | Filters rows before grouping or aggregation; used for non-aggregated conditions. |
| **HAVING** | Filters groups after aggregation; used with GROUP BY. |
| **AND** | Combines multiple conditions (all must be true). |
| **OR** | Combines conditions where at least one must be true. |
| **NOT** | Negates a condition. |
| **IN** | Checks if a value exists within a list of values. |
| **NOT IN** | Checks if a value does NOT exist in a list. |
| **BETWEEN** | Filters values within a given inclusive range. |
| **LIKE** | Filters rows based on pattern matching using `%` or `_`. |
| **NOT LIKE** | Opposite of LIKE; excludes matching patterns. |
| **IS NULL** | Returns rows where the column value is NULL. |
| **IS NOT NULL** | Returns rows where the column value is NOT NULL. |
| **EXISTS** | Returns rows where a subquery produces at least one result. |
| **ANY / SOME** | Compares a value with ANY value in a list or subquery. |
| **ALL** | Compares a value with ALL values in a list or subquery. |








