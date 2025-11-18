 ### A Clear and Detailed Explanation of Fundamental Database Concepts

## 1 Introduction

Databases are essential components of modern applications. SQL (Structured Query Language) enables efficient **storage, retrieval, processing, and management** of data.

To design scalable, consistent, and high-performance systems, it is important to understand concepts like **ACID**, **CAP theorem**, **Joins**, **Transactions**, **Indexes**, and more.

This technical paper explains all essential SQL concepts.

---

## 2 ACID Properties

ACID stands for **Atomicity, Consistency, Isolation, Durability**.

### **2.1 Atomicity**
- A transaction should execute **fully or not at all**.
- If part of the transaction fails, all changes must be rolled back.
### **2.2 Consistency**
- A transaction must keep the database in a **valid state** after execution.
- Ensures the database moves from one valid state to another valid state.
- Constraints, triggers, and rules must remain valid.
### **2.3 Isolation**
- Multiple transactions should not interfere with each other.
- Each transaction must run as if it is the **only** transaction.
- Prevents interference between concurrent transactions.
### **2.4 Durability**
- Once committed, data should be **permanently stored**.
- After a transaction is committed, the results are permanently saved.
- Even if a system failure occurs afterwards, committed data is not lost.
---
## 3 CAP Theorem
A distributed database can guarantee only **two** of the following three:
### **3.1 Consistency (C)**
- All nodes return the **same, most recent** data.
### **3.2 Availability (A)**
- Every request gets a response, even during failures.
### **3.3 Partition Tolerance (P)**
- System continues working despite **network failures**.
> **You can choose only two: CP, AP, or CA (not possible in distributed systems).**
---
## 4 Joins in SQL
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
---
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

### 5.3 Combining Filters + Aggregation
Useful for real-world analytics.
Example:
```sql
SELECT product_id, SUM(quantity) AS total_quantity
FROM sales
WHERE order_date >= '2024-01-01'
GROUP BY product_id
HAVING SUM(quantity) > 100
ORDER BY total_quantity DESC;
```
---
## 6 Database Normalization 
Ensuring Efficient, Consistent, and Structured Database Design
### 6.1 Introduction
Normalization is a systematic process of organizing data in a relational database.  
Its main goals are:
- To **eliminate redundancy** (duplicate data)
- To **ensure data integrity**
- To **reduce update, insert, and delete anomalies**
- To create a **well-structured, efficient database schema**
Normalization breaks large, complex tables into smaller ones while maintaining relationships between them using **keys**.
Normalization is essential for designing efficient, scalable, and error-free relational databases.  
By applying **1NF → 2NF → 3NF → BCNF**, you:
- Keep data clean  
- Remove anomalies  
- Improve consistency  
- Create a logical database structure  
These principles form the foundation of SQL database design and are widely used in real-world systems.
### 6.2 Why Normalization is Important
Before understanding forms, it’s important to know why normalization is used:
- Prevents **duplicate data**
- Ensures **accurate** and **consistent** records
- Makes updates safer and faster
- Reduces unnecessary usage of storage
- Improves **query performance**
- Simplifies maintenance and future database changes
### 6.3 Types of Normal Forms
Normalization is performed in stages called **Normal Forms (NF)**.  
Each stage solves specific data problems.
Below are the most widely used forms:  
**1NF, 2NF, 3NF, and BCNF.**
#### 1. First Normal Form (1NF)
A table is in **1NF** when:
- All column values are **atomic** (indivisible)
- No repeating groups or arrays
- Each record must be unique
#### Example:
```
Not in 1NF:
| Student | Subjects        |
|---------|-----------------|
| Hima    | Math, English   |

 Correct (1NF Applied):
| Student | Subject  |
|---------|----------|
| Hima    | Math     |
| Hima    | English  |
```
#### 2. Second Normal Form (2NF)
A table is in **2NF** when:
- It is already in **1NF**
- No **partial dependency** exists  
  (i.e., no non-key attribute depends on part of a composite primary key)
#### Example:
```
Not in 2NF:
Primary Key = (StudentID, CourseID)

| StudentID | CourseID | StudentName |
|-----------|----------|-------------|
`StudentName` depends only on `StudentID`, not the whole key → partial dependency.

Correct (After 2NF):
Split table:
**Students Table**
| StudentID | StudentName |

**Courses Table**
| CourseID | … |

**Enrollment Table**
| StudentID | CourseID |
```
#### 3. Third Normal Form (3NF)
A table is in **3NF** when:
- It is already in **2NF**
- No **transitive dependency** exists  
  (non-key attribute should not depend on another non-key attribute)
#### Example:
```
Not in 3NF:
| EmpID | EmpName | DeptID | DeptName |
|-------|---------|--------|----------|

`DeptName` depends on `DeptID` → transitive dependency.

Correct (After 3NF):

**Employees Table**
| EmpID | EmpName | DeptID |

**Departments Table**
| DeptID | DeptName |
```
#### 4. Boyce–Codd Normal Form (BCNF)
A stricter version of 3NF.  
A table is in **BCNF** if:
- For every functional dependency **A → B**,  
  **A must be a super key**.
#### Used when:
- There are overlapping candidate keys
- Complex dependencies exist
BCNF ensures maximum consistency.

#### 5. Higher Normal Forms (Advanced)
Not commonly used in most applications, but used in special cases.
#### 4NF – Fourth Normal Form
- Eliminates **multi-valued dependencies**
#### 5NF – Fifth Normal Form
- Eliminates **join dependency issues**  
- Ensures tables cannot be decomposed further without losing information
### 6.4 Drawbacks of Normalization
Normalization has some trade-offs:
- More **JOIN operations** in queries  
- Complex schema
- Sometimes slower reads (OLAP systems often use denormalization)
### 6.5 Example Summary Table
| Normal Form | What It Fixes | Rule |
|--------------|----------------|------|
| **1NF** | Repeating groups, non-atomic data | Atomic values only |
| **2NF** | Partial dependencies | Full key dependency |
| **3NF** | Transitive dependencies | Non-key attributes depend only on key |
| **BCNF** | Advanced functional dependency exceptions | Left side must be a superkey |

---
## 7 Indexes in SQL  
Improving Query Performance with Efficient Data Access
### 7.1 Introduction
Indexes in SQL are special data structures used to **speed up data retrieval** operations.  
They work like the index of a book—helping the database quickly locate the required rows without scanning the entire table.
Indexes improve performance for **SELECT** queries but may slightly slow down **INSERT**, **UPDATE**, and **DELETE** because the index must also be updated.
### 7.2 Why Indexes Are Needed
- Faster search and retrieval  
- Efficient lookups on large tables  
- Rapid sorting and filtering  
- Speeding up JOIN operations  
- Improving performance for WHERE, ORDER BY, and GROUP BY queries  
Without indexes, databases use **full table scans**, which are slow.
### 7.3 How Indexes Work
Internally, most relational databases use **B-Tree** or **Hash** structures.
- **B-Tree Indexes** → Balanced tree structure used for range queries and ordering.  
- **Hash Indexes** → Used for fast equality lookups (`=` operator).  
Indexes store:
- The **key (indexed column)**  
- A pointer to the actual row in the table  
### 7.4 Types of Indexes
| Index Type | Description | Example |
|------------|-------------|---------|
| **Primary Index** | Automatically created on the PRIMARY KEY column; ensures uniqueness. | `id INT PRIMARY KEY` |
| **Unique Index** | Ensures all values in a column are unique (no duplicates). | `CREATE UNIQUE INDEX idx_email ON users(email);` |
| **Non-Unique Index** | Regular index used to speed up queries but allows duplicate values. | `CREATE INDEX idx_lastname ON employees(last_name);` |
| **Composite Index** | Index created on two or more columns; improves multi-column searches. | `CREATE INDEX idx_name_age ON users(name, age);` |
| **Full-Text Index** | Enables fast searches on large text fields. | `CREATE FULLTEXT INDEX idx_desc ON products(description);` |
| **Hash Index** | Fast lookups for equality comparisons (`=`). Mainly used in some DB engines. | N/A (engine-specific) |
| **Spatial Index** | Used for geographic or spatial data types (GIS data). | N/A (engine-specific) |
### 7.5 When to Use Indexes
Use indexes when columns are involved in:
- **WHERE** conditions  
- **JOIN** conditions  
- **ORDER BY**  
- **GROUP BY**  
- **Frequent lookups**
#### Example:
```sql
SELECT * FROM users WHERE email = 'hima@gmail.com';
```
### 7.6 When NOT to Use Indexes
Avoid creating indexes on:
- **Small tables** (full table scan is already fast)
- **Columns that frequently change** (INSERT/UPDATE become slower)
- **Columns with many duplicate values** (e.g., TRUE/FALSE, gender)
- **Columns rarely used in search conditions** (index becomes useless)
---
## 8 Transactions in SQL  
### 8.1 Introduction
A **transaction** in SQL is a sequence of one or more statements executed as a single logical unit of work.  
Transactions ensure that data remains **accurate, consistent, and reliable**, even in the presence of errors, failures, or multiple users accessing the database simultaneously.
Transactions follow the important **ACID** principles
Typical examples of transactions include:
- Money transfers
- Inserting or updating multiple related rows
- Booking systems (seats, tickets, slots)
- Inventory updates
### 8.2 Transaction Control Commands (TCL)
SQL provides commands to manage transactions.
#### 1 BEGIN / START TRANSACTION**
Starts a new transaction.
#### EXAMPLE :
```sql
BEGIN;
-- or
START TRANSACTION;
```
#### 2 COMMIT
Saves all changes of the transaction permanently.
```
COMMIT;
```
#### 3 ROLLBACK
Undoes all changes made in the current transaction.
```
ROLLBACK;
```
#### 4 SAVEPOINT
Creates a checkpoint that you can roll back to.
```
SAVEPOINT point1;
ROLLBACK TO point1;
```
#### Example: Bank Money Transfer Transaction
```
Without Transaction (Risky)
UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;

If the second query fails, the money is lost.

With Transaction (Safe)
BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;
COMMIT;

If any statement fails:
ROLLBACK;

Guarantees all-or-nothing execution.
```
### 8.3 Real-World Use Cases of Transactions
- **Banking** : Money transfer operations need atomicity and consistency.
- **E-commerce** :Order processing, inventory updates, and payments rely on transactions.
- **Reservation** Systems:Hotel rooms, seats, tickets must be locked and committed safely.
- **Financial Applications**:All accounting systems use transaction-based processing.

---
## 9 Locking Mechanism in Databases  
Ensuring Safe and Concurrent Data Access
### 9.1 Introduction
In multi-user database systems, multiple transactions often try to access or modify the same data at the same time.  
To prevent conflicts, data corruption, and inconsistent results, databases use a **locking mechanism**.
A lock ensures that **only authorized transactions can read/write** a particular piece of data at any given moment.
The locking mechanism is essential for maintaining data integrity in transactional databases.
    - It ensures safe multi-user access by:
    - Preventing conflicts
    - Avoiding data corruption
    - Supporting isolation levels
    - Ensuring consistency through controlled access
### 9.2 Why Locking is Required
Locking prevents issues such as:
- **Dirty reads** (reading uncommitted data)
- **Lost updates** (one transaction overwrites another)
- **Non-repeatable reads** (same query returns different results)
- **Phantom reads** (new rows appear between reads)
- **Data corruption** during concurrent writes
Locks maintain **data consistency and integrity** in multi-user environments.
### 9.3 Types of Locks
#### 1 Shared Lock (Read Lock)
- Allows multiple transactions to **read** the same data.
- Prevents other transactions from writing to the data.
- Many readers → **shared** access.
#### Example:
If Transaction A reads a row using a shared lock:
- Transaction B can read it (shared lock)
- Transaction B **cannot write** to it (needs an exclusive lock)
#### 2 Exclusive Lock (Write Lock)
- Only one transaction can acquire an exclusive lock.
- Blocks both reads and writes from other transactions.
- Used when modifying data.
#### Example:
If Transaction A updates a row:
- Transaction B cannot read or write that row until lock is released.
#### 3 Update Lock
- Used to prevent deadlocks.
- Applied when a transaction **intends to modify** a row but has not yet written to it.
- Ensures only one transaction can prepare for an update at a time.
#### 4 Intent Locks
Intent locks indicate a transaction’s future locking behavior on child nodes in a hierarchy.
- **Intent Shared (IS)** – Plans to place shared locks at a lower level  
- **Intent Exclusive (IX)** – Plans to place exclusive locks at a lower level  
- **Shared Intent Exclusive (SIX)** – Combination lock  
These locks help avoid conflicting lock requests in hierarchical systems (like table → row)
### 9.4 Lock Granularity
Databases can lock resources at different levels:
#### 1 Row-Level Lock
- Locks only the specific row.
- Best for high concurrency.
- Most common in OLTP systems.
#### 2 Table-Level Lock
- Locks the entire table.
- Faster but reduces concurrency.
#### 3 Page-Level Lock
- Locks a fixed-size block of data (like 8KB page).
- Balance between row and table level.
#### 4 Database-Level Lock
- Rare; used during backups or maintenance.
### 9.5 Locking Modes in SQL Databases
| Lock Mode | Purpose |
|-----------|---------|
| **Shared (S)** | Read-only access |
| **Exclusive (X)** | Write operations |
| **Update (U)** | Prevent deadlocks during updates |
| **Intent Shared (IS)** | Intend to acquire shared lock on row/page |
| **Intent Exclusive (IX)** | Intend to acquire exclusive lock on row/page |
| **Shared Intent Exclusive (SIX)** | Read entire table, update specific rows |

### 9.6 Deadlocks
A **deadlock** occurs when two transactions wait for each other’s locks, causing both to be stuck.
#### Example:
```
- Transaction A locks row 1, wants row 2  
- Transaction B locks row 2, wants row 1  
Database resolves deadlocks by:
- Detecting the deadlock
- Rolling back one transaction (the "victim")
```
### 9.7 Locking vs Isolation Levels
Isolation levels determine **how strictly locking is applied**.
| Isolation Level | Locking Strictness |
|-----------------|--------------------|
| Read Uncommitted | Minimal locking |
| Read Committed | Prevents dirty reads |
| Repeatable Read | Prevents non-repeatable reads |
| Serializable | Strictest locking, prevents phantom reads |

Higher isolation → more locking → fewer concurrency issues → slower performance.
### 9.8 Lock Duration
- **Short-term locks**: Held for the duration of a statement  
- **Long-term locks**: Held for entire transaction until COMMIT or ROLLBACK  

Example:
```sql
BEGIN;

UPDATE accounts SET balance = balance - 100 WHERE id = 1;
-- Lock stays until COMMIT

COMMIT;  -- Lock released
```
---
## 10 Database Isolation Levels  
### 10.1 Introduction
Database Isolation Levels define **how transactions interact with each other** when running at the same time.  
They decide how much one transaction is allowed to "see" the work of another transaction.
The goal of isolation levels is to balance:
- **Data accuracy** (consistency)
- **Performance** (speed and concurrency)
Different isolation levels offer different protections against common problems.

### 10.2 Problems That Isolation Levels Prevent
#### 1.Dirty Read
Reading data that another transaction has written but not committed.
#### 2.Non-Repeatable Read
Same query returns different results within the same transaction.
#### 3 Phantom Read**
New rows appear between two reads of the same query.

### 10.3 Isolation Levels in SQL
SQL defines **four standard isolation levels**.
#### 1. Read Uncommitted  
- Lowest isolation level  
- Allows **dirty reads**  
- Fast but unsafe
```
  Problems Allowed:
- Dirty Read ✔  
- Non-Repeatable Read ✔  
- Phantom Read ✔  
  Use Case:
- Only for read-only analytics (rarely recommended)
  ```
#### 2. Read Committed  
- Most commonly used level (default in many databases)  
- A transaction can read only **committed** data  
``` Problems Allowed:
- Dirty Read ✖  
- Non-Repeatable Read ✔  
- Phantom Read ✔  
  Use Case:
- Good balance between safety and performance
 ```
#### 3. Repeatable Read  
- Ensures the same query returns the same result within a transaction  
- Prevents non-repeatable reads
```
 Problems Allowed:
- Dirty Read ✖  
- Non-Repeatable Read ✖  
- Phantom Read ✔  
 Use Case:
- Banking, booking systems, consistent reads
  ```
#### 4. Serializable  
- Highest isolation  
- Transactions execute as if they ran **one after another**  
- Strict but slowest
```
 Problems Allowed:
- Dirty Read ✖  
- Non-Repeatable Read ✖  
- Phantom Read ✖  
Use Case:
- Critical financial systems  
- Data must always be correct  
```
### 10.4 Comparison Table

| Isolation Level     | Dirty Read | Non-Repeatable Read | Phantom Read |
|---------------------|------------|----------------------|--------------|
| Read Uncommitted    | Yes        | Yes                  | Yes          |
| Read Committed      | No         | Yes                  | Yes          |
| Repeatable Read     | No         | No                   | Yes          |
| Serializable        | No         | No                   | No           |

### 10.5 How to Set Isolation Level (Example)
```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```
---
## 11 Database Triggers  
### 11.1 Introduction
A **Trigger** is a special database object that automatically executes in response to a specific event on a table.  
Triggers automate actions in the database whenever INSERT, UPDATE, or DELETE occurs.
They improve consistency, enforce business rules, and reduce repetitive code.
However, they should be used wisely to avoid performance issues and hidden logic.
Triggers help enforce rules, maintain data integrity, and automate actions without manual execution.
Triggers are activated by:
- **INSERT**
- **UPDATE**
- **DELETE**
They run automatically **before** or **after** these operations.
### 11.2 Why Triggers Are Used
Triggers help in:
- Maintaining **data consistency**
- Enforcing **business rules**
- Creating logs or history tables
- Validating data before saving
- Automating system tasks (timestamps, audits)
### 11.3 Types of Triggers
#### 1. BEFORE Trigger
Executes **before** the event occurs.  
Useful for:
- Validating data  
- Modifying input values  
- Preventing unwanted changes  
**Example:**
```sql
CREATE TRIGGER validate_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary < 0 THEN
        SET NEW.salary = 0;
    END IF;
END;
```
#### 2. AFTER Trigger
Executes after the event occurs.
Useful for:
Logging
Sending notifications
Updating related tables
**Example:**
```sql
CREATE TRIGGER log_insert
AFTER INSERT ON orders
FOR EACH ROW
INSERT INTO order_logs(order_id, created_at)
VALUES (NEW.id, NOW());
```
#### 3. INSERT Trigger
Runs when a row is inserted.
**Example:**
```sql
CREATE TRIGGER add_timestamp
BEFORE INSERT ON users
FOR EACH ROW
SET NEW.created_at = NOW();
```
#### 4. UPDATE Trigger
Runs when a row is updated.
**Example:**
```sql
CREATE TRIGGER update_timestamp
BEFORE UPDATE ON users
FOR EACH ROW
SET NEW.updated_at = NOW();
```
#### 5. DELETE Trigger
Runs when a row is deleted.
**Example:**
```sql
CREATE TRIGGER backup_before_delete
BEFORE DELETE ON employees
FOR EACH ROW
INSERT INTO employees_backup VALUES (OLD.id, OLD.name, OLD.salary);
```
#### 6.DROP Trigger
**Example:** How to Drop a Trigger
```sql
DROP TRIGGER IF EXISTS log_insert;
```
### 11.4 Use Cases of Triggers
**Audit logs**
Track who changed what and when.
**Auto-updating timestamps**
Automatically set created_at or updated_at.
**Data validation**
Reject invalid values before inserting or updating.
**Maintaining history**
Before deleting, save data in an archive table.
**Cascading operations**
Update related records when a parent record changes.

---
## References
PostgreSQL Official Documentation – Locking & Concurrency
https://www.postgresql.org/docs/current/explicit-locking.html





