# SQL Concepts

***
>### TOPICS

>*:point_right: [ACID](#1)*
>*:point_right: [CAP Theorem](#2)*
>*:point_right: [Joins](#3)*
>*:point_right: [Aggregations, Filters in queries](#4)*
>*:point_right: [Normalization](#5)*
>*:point_right: [Indexes](#6)*
>*:point_right: [Transactions](#7)*
>*:point_right: [Locking mechanism](#8)*
>*:point_right: [Database Isolation Levels](#9)*
>*:point_right: [Triggers](#10)*

***
<a id="1"></a>

## ACID

>In large database, there are lots of change happen and those changes are called as **Transactions**.
To ensure the reliability and consistency of database transactions, DBMS follow certain set of properties which are know as **ACID Properties in DBMS**.

### 1. Atomicity (A):

-   Atomicity ensures that a transaction is treated as a single, indivisible unit of work.
-   Either all the operations within a transaction are successfully completed, or none of them are.
-   If any part of a transaction fails, the entire transaction is rolled back to its previous state, ensuring that the database remains in a consistent state.

### 2. Consistency ( C ):

-   Consistency ensures that a transaction brings the database from one consistent state to another consistent state.
-   It enforces integrity constraints, ensuring that the data remains valid and adheres to predefined rules or constraints.
-   If a transaction violates any constraints, it is rolled back, preserving the consistency of the database.

### 3. Isolation (I):

-   Isolation ensures that concurrent transactions do not interfere with each other.
-   Transactions appear to execute in isolation, as if they are the only transactions running.
-   This property prevents issues like dirty reads and non-repeatable reads.

### 4. Durability (D):

-   Durability guarantees that once a transaction is committed, its changes are permanent.
-   These changes are stored in non-volatile storage so that they can be recovered upon system restart.
-   Durability ensures that committed data is not lost and maintains the reliability of the database.
***
***
<a id="2"></a>

## CAP Theorem

>The CAP theorem, also known as Brewer's theorem, CAP theorem is a concept that primarily applies to distributed databases and distributed systems.

### 1. Consistency ( C ):
- SQL databases are designed to provide strong consistency.    
- When you perform a transaction in an SQL database, 
    it ensures that all data changes are committed atomically,
    and all subsequent transactions see a consistent state of the data.
-   In the face of network partitions or failures, SQL databases often choose to become unavailable to maintain this strong consistency.
    
### 2. Availability (A):
    
-   SQL databases, especially in a distributed setup, may prioritize consistency over availability.
-   During normal operations, SQL databases are available for reads and writes.
-   However, in cases of network partitions or severe failures, SQL databases may become temporarily unavailable to avoid compromising data consistency.
    
### 3. Partition Tolerance (P):
    
-   SQL databases are generally partition-tolerant to some extent.
-   They can continue to operate in the presence of network partitions but may choose to become unavailable to maintain consistency.
-   The level of partition tolerance can vary depending on the specific database system.

> **In SQL Database, mainly we see CA and CP combinations.**
***
***
<a id="3"></a>

## Joins

>Joins are a fundamental operation in RDBMS that allow you to combine data from multiple tables based on a related column between them.

There are following types of joins commonly used in SQL:
### 1.INNER JOIN:
    
-   An INNER JOIN returns only the rows that have matching values in both tables.
-   It filters out rows where there is no match between the specified columns in the joined tables.
-   Syntax: `SELECT * FROM table1 INNER JOIN table2 ON table1.column = table2.column;`
### 2.LEFT JOIN:
    
-   A LEFT JOIN returns all rows from the left table and the matched rows from the right table.
-   If there is no match for a row in the left table, NULL values are returned for columns from the right table.
-   Syntax: `SELECT * FROM table1 LEFT JOIN table2 ON table1.column = table2.column;`
### 3.RIGHT JOIN:
    
-   A RIGHT JOIN is similar to a LEFT JOIN but returns all rows from the right table and the matched rows from the left table.
-   If there is no match for a row in the right table, NULL values are returned for columns from the left table.
-   Syntax: `SELECT * FROM table1 RIGHT JOIN table2 ON table1.column = table2.column;`
### 4.FULL JOIN:
    
-   A FULL JOIN returns all rows from both tables and includes NULL values where there is no match in either table.
-   It combines the results of a LEFT JOIN and a RIGHT JOIN.
-   Syntax: `SELECT * FROM table1 FULL JOIN table2 ON table1.column = table2.column;`
### 5.SELF JOIN:
    
-   A SELF JOIN is used to join a table with itself.
-   It is helpful when you have hierarchical or related data within a single table.
-   Syntax: `SELECT * FROM table1 t1 INNER JOIN table1 t2 ON t1.column = t2.column;`
### 6.CROSS JOIN:
    
-   A CROSS JOIN combines every row from the first table with every row from the second table.
-   It does not require an ON clause since it returns all possible combinations.
-   Syntax: `SELECT * FROM table1 CROSS JOIN table2;`
***
***
<a id="4"></a>

## Aggregations, Filters in queries

>Aggregations and filters are components of SQL queries used to manipulate and extract specific information from a database.

### Aggregations:

>Aggregations are SQL functions that perform calculations on sets of values and return a single.

Some common SQL aggregation functions include:

1.  **COUNT():**
    
	   -   Counts the number of rows that match a specific condition.
    -   Example:  `SELECT COUNT(*) FROM employees;`
2.  **SUM():**
    
	   -   Add numeric values in a specified column.
    -   Example: `SELECT SUM(salary) FROM sales;`
3.  **AVG():**
    
	   -   Calculates the average of numeric values in a specified column.
    -   Example: `SELECT AVG(price) FROM products;`
4.  **MAX():**
    
	   -   Returns the maximum value in a specified column.
    -   Example: `SELECT MAX(score) FROM students;`
5.  **MIN():**
    
	   -   Returns the minimum value in a specified column.
    -   Example: `SELECT MIN(age) FROM customers;`
6.  **GROUP BY:**
    
	   -   Groups rows with similar values in one or more columns together and allows you to perform aggregations within each group.
    -   Example: `SELECT department, AVG(salary) FROM employees GROUP BY department;`
 
### Filters:

>Filters are used to filter the rows returned by a SQL query based on specified conditions. You can apply filters using the *WHERE* in your SQL query. 

Here are some commonly used SQL operators and techniques for filtering data:

1.  **WHERE:**
    
    -   The WHERE allows you to specify conditions that must be met for a row to be included in the query result.
    -   Example: `SELECT * FROM orders WHERE order_date > '2023-01-01';`
2.  **Comparison Operators:**
    
    -   SQL supports operators like **=**, **<**, **>**, **<=**, **>=**, and **<>** to compare values.
    -   Example: `SELECT * FROM products WHERE price > 50;`
3.  **Logical Operators:**
    
    -   You can use logical operators such as *AND*, *OR*, and *NOT* to combine multiple conditions in the WHERE.
    -   Example: `SELECT * FROM customers WHERE age >= 18 AND city = 'New York';`
4.  **IN Operator:**
    
    -   The *IN* operator allows you to specify a list of values to match in a column.
    -   Example: `SELECT * FROM employees WHERE department IN ('Sales', 'Marketing');`
5.  **LIKE Operator:**
    
    -   The LIKE operator is used for pattern matching **%**  multiple characters, **_** for a single character.
    -   Example: `SELECT * FROM products WHERE product_name LIKE 'Apple%';`
6.  **BETWEEN Operator:**
    
    -   The *BETWEEN* operator is used to filter rows within a range of values.
    -   Example: `SELECT * FROM orders WHERE order_date BETWEEN '2023-01-01' AND '2023-12-31';`
7.  **IS NULL Operator:**
    
    -   The *IS NULL* operator checks for NULL values in a column.
    -   Example: `SELECT * FROM customers WHERE email IS NULL;`
   
***
***
<a id="5"></a>

## Normalization

>Normalization is a database design process that involves organizing and structuring a relational database to minimize data redundancy and improve data integrity.
The primary goal of normalization is to break down a large, complex table into smaller, related tables while maintaining data relationships using foreign keys.

Here's an overview of the common normalization forms:

### 1.First Normal Form (1NF):
    
-   Ensures that each column in a table contains only atomic values.
-   Eliminates repeating groups by creating separate rows for each related data item.
-   Example: If you have a **Book** table with a column for **Authors**, it should not store multiple author names in a single cell but instead have multiple rows for each book-author pair.

### 2.Second Normal Form (2NF):
    
-   Builds upon 1NF and eliminates partial dependencies.
-   A table is in 2NF if it is in 1NF and all non-key attributes are fully functionally dependent on the primary key.
-   It often involves splitting tables and creating relationships using foreign keys.
-   Example: Splitting a **Sales** table into **Orders** and **OrderDetails** tables to eliminate partial dependencies.

### 3.hird Normal Form (3NF):
    
-   Builds upon 2NF and eliminates transitive dependencies.
-   A table is in 3NF if it is in 2NF, and all non-key attributes are transitively dependent on the primary key.
-   Like 2NF, it involves creating additional tables and foreign key relationships.
-   Example: Splitting a **Customers** table into **Customers** and **CustomerAddresses** tables to remove transitive dependencies.

### 4.Boyce-Codd Normal Form (BCNF):
    
-   A more advanced form of normalization that eliminates all partial and transitive dependencies.
-   It is stricter than 3NF and may require additional restructuring of tables.
-   Ensures that every determinant (a column that uniquely determines another column) is a superkey (a set of columns that uniquely identifies a row).
-   Example: Refining relationships between tables to achieve BCNF when 3NF is insufficient.

### 5.Fourth Normal Form (4NF) and Beyond:
    
-   These forms address more complex situations involving multi-valued and join dependencies.
-   They are typically used in highly specialized cases and may require advanced database design techniques.
  
 > **The choice of which normalization form to apply depends on the specific requirements and complexity of your data and application.**
  ***
  ***
  <a id="6"></a>
  
  ## Indexes
  
  >Indexes are database objects that improve the speed of data retrieval on database tables. They work by providing a data structure that allows the DBMS to quickly locate and access the rows of a table based on the values in one or more columns. Without indexes, database queries require a full table scan, which can be slow, especially for large datasets.
  ***
  ***
<a id="7"></a>

## Transactions

>A transaction in the context of DBMS is a logical unit of work that consists of one or more database operations. These operations can include inserting, updating, deleting, or reading data from a database. Transactions are essential for maintaining data integrity and ensuring that the database remains in a consistent state, even in the presence of failures or concurrent access by multiple users.

A transaction goes through various states, typically represented as follows:

**Active:** The initial state when the transaction is executing.
**Partially Committed:** The transaction has completed its execution but has not been fully committed yet.
**Committed:** The transaction has been successfully executed and permanently saved in the database.
**Aborted/Rolled Back:** The transaction is canceled due to an error or explicit rollback.
***
***
<a id="8"></a>

## Locking Mechanism

>Locking mechanisms are component of DBMS used to control and coordinate concurrent access to tables, rows, or other data objects. These mechanisms prevent multiple transactions from accessing or modifying the same data simultaneously, which helps maintain data consistency and integrity. 

There are several types of locks and locking mechanisms used in DBMS:

1.  **Shared Lock (S-lock):**
    
    -   Multiple transactions can hold shared locks on the same resource.
    -   Shared locks are used when a transaction wants to read data without modify it.
    -   Other transactions can also acquire shared locks on the same resource, allowing for concurrent reading.

2.  **Exclusive Lock (X-lock):**
    
    -   Only one transaction can hold an exclusive lock on a resource at a time.
    -   Exclusive locks are used when a transaction intends to modify data.
    -   While an exclusive lock is held, no other transactions can acquire either shared or exclusive locks on the same resource.

3.  **Intent Lock:**
    
    -   Intent locks are higher-level locks that indicate the intention of a transaction to acquire lower-level locks.
    -   They serve as a signal to other transactions about the intent of a transaction on a resource.
    -   For example, an intent shared lock indicates that a transaction intends to acquire shared locks, while an intent exclusive lock indicates an intent to acquire exclusive locks.

4.  **Row-Level Locks:**
    
    -   Row-level locks allow locking individual rows within a table.
    -   They are more fine-grained than table-level locks and enable multiple transactions to modify different rows in the same table concurrently.

5.  **Table-Level Locks:**
    
    -   Table-level locks lock the entire table, preventing any transactions from accessing it until the lock is released.
    -   While effective at preventing concurrent access, they can lead to contention and reduced concurrency.

6.  **Deadlock Detection and Resolution:**
    
    -   Deadlocks occur when two or more transactions are waiting for locks held by each other, causing them to be stuck indefinitely.
    -   DBMSs use deadlock detection and resolution algorithms to identify and break deadlocks.

7.  **Lock Timeout:**
    
    -   Some systems allow you to specify a timeout for how long a transaction is willing to wait for a lock.
    -   If a lock cannot be acquired within the specified timeout, the transaction may be aborted or rolled back.

8.  **Lock Escalation:**
    
    -   Lock escalation is a process where a DBMS may automatically escalate row-level locks to a table-level lock when a transaction acquires too many row-level locks.
    -   This helps reduce the overhead of managing many locks.

***
***
<a id="9"></a>

## Database Isolation Levels


>Database isolation levels are define how transactions interact with each other in a multi-user environment. These isolation levels determine the visibility and behavior of data modified by one transaction to other transactions running concurrently.

There are four standard isolation levels, each with a different degree of data isolation and concurrency:

1.  **Read Uncommitted (Isolation Level 0):**
    
    -   In this isolation level, transactions are not isolated from each other at all.
    -   A transaction can see uncommitted changes made by other transactions, which can lead to dirty reads, non-repeatable reads, and phantom reads.
    -   It offers the highest level of concurrency but the lowest level of data consistency and integrity.
    -   Generally not recommended for most applications due to its potential data integrity issues.
2.  **Read Committed (Isolation Level 1):**
    
    -   In this isolation level, transactions are isolated from uncommitted changes made by other transactions.
    -   A transaction can only see committed changes, preventing dirty reads.
    -   However, non-repeatable reads and phantom reads are still possible.
    -   Read Committed is a common isolation level used in many database systems by default.
3.  **Repeatable Read (Isolation Level 2):**
    
    -   In this isolation level, transactions are further isolated from changes made by other transactions.
    -   A transaction can see only committed changes as they existed at the start of the transaction.
    -   This prevents dirty reads and non-repeatable reads.
    -   However, phantom reads can still occur, as new rows may be inserted by other transactions.
4.  **Serializable (Isolation Level 3):**
    
    -   Serializable is the highest isolation level and provides the strongest guarantees for data consistency and integrity.
    -   In this isolation level, transactions are completely isolated from each other, and the database ensures that all concurrent transactions behave as if they are executed sequentially.
    -   Serializable transactions prevent dirty reads, non-repeatable reads, and phantom reads.
    -   Achieving this isolation level may require locking or other mechanisms that can reduce concurrency.

    ***
    ***
<a id="10"></a>

## Triggers

>Triggers are database objects that are used to automatically execute a set of predefined SQL statements in response to specific events or conditions occurring in a database. These events or conditions can include data changes *(INSERT, UPDATE, DELETE)* or specific database operations *(CREATE, ALTER, or DROP)*.

###Types of Triggers:

**DML Triggers:** These triggers fire in response to data manipulation language (DML) operations such as INSERT, UPDATE, or DELETE statements on a table.

**DDL Triggers:** These triggers fire in response to data definition language (DDL) events like CREATE, ALTER, or DROP statements for tables, views, or other database objects.

>*Triggers provide a mechanism for automating database-related tasks and ensuring data consistency and integrity. When used appropriately, triggers can enhance the functionality and reliability of a database system.*