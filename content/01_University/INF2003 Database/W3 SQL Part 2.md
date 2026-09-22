# Data Manipulation Language (DML): INSERT

> Adding new rows to the existing table, order sensitive

## Insert
```SQL
INSERT INTO table_name (col3, col5, ...)
VALUES (val3, val5, ...);
```


## Update
> UPDATE modify the existing records in a table

```SQL
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE [condition];
```


## Delete
> DELETE the existing records from a table

```SQL
DELETE FROM table_name
WHERE [condition];
```

## Select
```SQL
SELECT col1, col2, ...
FROM table_name
WHERE condition;
```

### If really want to remove duplication
```SQL
SELECT DISTINCT A1, A2
```


##### Sailors
| sid | name   | rating | age |
| --- | ------ | ------ | --- |
| 22  | Dustin | 7.5    | 45  |
| 31  | Lubber | 8.0    | 55  |
| 58  | Rusty  | 9.0    | 35  |
| 74  | Rusty  | 7.5    | 35  |

1. Find the **name** and **age** of **all** sailors.
> [!Answer 1]-
> ```SQL
> SELECT name, age
> FROM Sailors;
> ```

2. Find **distinct** **name** and **age** of all sailors
> [!Answer 2]-
> ```SQL
> SELECT DISTINCT name, age
> FROM Sailors;
> ```

3. Find all **sailors** with **rating** **higher** than **7.8**
> [!Answer 3]-
> ```SQL
> SELECT name, age
> FROM Sailors
> WHERE rating > 7.8;
> ```

4. Find **all sailors** with rating **7.8**
> [!Answer 4]-
> ```SQL
> SELECT name, age
> FROM Sailors
> WHERE rating = 7.8;
> ```

## SELECT with arithmetic operations
- Use aliases to generate a temporary name
	- Useful when involving a table more than once
	- Keyword 'AS' is optional

```SQL
SELECT sid, name, rating/2 AS new_rating, age
FROM Sailors;
```

![[Pasted image 20260922192457.png]]


## Rename
- Can specify alternate names in **FROM** clause
	- Syntax: table AS name
	- **AS** is optional but clearer to leave it in
	- Useful for referencing long table name
	- When table is renamed in FROM, the new name can be used in **both** `SELECT` and `WHERE` clauses

```SQL
SELECT c.cust_name, l.amount
FROM customer AS c, borrower AS b, loan AS l
WHERE c.cust_name = b.cust_name AND b.loan_id = l.loan_id;
```


## ORDER BY
- SQL result is unsorted by default
- Sort: if multiple attributes, must have an **order** of the **attributes**
- **ORDER BY** < list of attributes >
	- By default: **Ascending**
	- Descending: ORDER BY DESC < list of attributes >
	- Normally **AFTER** `WHERE`, `GROUP BY`, and `HAVING`
		- For `GROUP BY`, performed in each group
	- Results: Passed to `SELECT` for output

- More advanced usage: `ORDER BY A+B DESC`
	- Order by the summation of the 2 components A and B

```SQL
SELECT  *
FROM Sailors
ORDER BY age DESC;

SELECT *
FROM Sailors
ORDER BY rating ASC, age DESC;
```


## WHERE with Multiple Tables

1. Find the **sid** of the sailors who have reserved a **red** boat
> [!Answer]-
> ```SQL
> SELECT R.sid
> FROM Reserves R, Boats B
> WHERE R.bid=B.bid AND B.color='red'
> ```

2. Find the **names** of the sailors who have reserved a **red** boat
> [!Answer]-
> ```SQL
> SELECT S.name
> FROM Sailors S, Reserves R, Boats B
> WHERE S.sid=R.sid AND R.bid=B.bid AND B.color="red"
> ```

### WHERE Advanced

1. **Add 0.5** to the ratings of the sailor who sailed **different boats** on the **same day**
> [!Answer]-
> ```SQL
> SELECT S.name, S.rating + 0.5 AS rating
> FROM Sailors S, Reserves R1, Reserves R2
> WHERE S.sid=R1.sid AND S.sid=R2.sid AND R1.day=R2.day
> AND R1.bid <> R2.bid
> ```

2. Find the **pair of sailors** where the former has **1.0 higher** rating than the later
> [!Answer]-
> ```SQL
> SELECT S1.name AS name1, S2.name AS name2
> FROM Sailors S1, Sailors S2
> WHERE S1.rating = S2.rating + 1.0
> ```


## UNION, INTERSECT, EXCEPT

### UNION
Find the **sid** of the sailors who have a **rating** of **10** **OR** reserved boat **104**
> [!Answer]-
> ```SQL
> SELECT S.sid
> FROM Sailors S
> WHERE S.rating = 10
> UNION
> SELECT R.sid
> FROM Reserves R
> WHERE R.bid - 104
> ```


### INTERSECT
Find **name** of sailors who reserved a **red** and a **green** boat
> [!Answer]-
> ```SQL
> SELECT S1.name
> FROM Sailors S1, Boats B1, Reserves R1
> WHERE S1.sid=R1.sid AND R1.bid=B1.bid AND B1.color="red"
> INTERSECT
> SELECT S2.name
> FROM Sailors S2, Boats B2, Reserves R2
> WHERE S2.sid=R2.sid AND R2.bid=B2.bid AND B2.color="green";
> ```


### EXCEPT (Set Difference)
Find the **sid** of sailors who've reserved **red** boat **BUT NOT** **green** ones.
> [!Answer]-
> ```SQL
> SELECT R.sid
> FROM Boats B1, Reserves R1
> WHERE R1.bid=B1.bid AND B1.color="red"
> EXCEPT
> SELECT R2.sid
> FROM Boats B2, Reserves R2
> WHERE R2.bid=B2.bid AND B2.color="green";
> ```


##### Characteristics
- By default: NO duplication for UNION in SQL, set operation
	- To retain duplicates, use UNION ALL
	- Similarly, INTERSECT ALL, and EXCEPT ALL
	- In terms of efficiency, with ALL is faster, as it doesn't need to remove duplicated ones


## Nested Queries
- Subquery embedded
- Multiple levels
- Typically in WHERE clause. Sometime also in FROM and HAVING clauses

Find the names of sailors who have reserved boat 103
> [!Answer]-
> ```SQL
> SELECT S.name
> FROM Sailors S
> WHERE S.sid IN
> 	(SELECT R.sid
> 	FROM Reserves R
> 	WHERE R.bid=103)
> ```


## Aggregate Operators
- Used to perform statistics
- `SUM()`: Returns sum or total of each group
- `COUNT()`: Returns number of rows of each group
- `AVG()`: Returns average and mean of each group
- `MIN()`: Returns minimum value of each group
- `MAX()`: Returns maximum value of each group
- Use `DISTINCT` for counting unique ones
- Can be applied to any columns


## Key Characteristics
> Aggregate functions compute a single value from a multiset of inputs

- The condition cannot include the aggregate
```SQL
# DONT DO THIS
SELECT name, n_visits
FROM guests
WHERE n_visits > AVG(n_visits)

# DO THIS
SELECT name, n_visits
FROM guests
WHERE n_visits > (
	SELECT AVG(n_visits)
	FROM guests
	);
```

### Mixing Aggregate function in SELECT clause
```SQL
# DONT DO THIS
SELECT name, MAX(age)
FROM Sailors

# DO THIS
SELECT MIN(age), MAX(age)
FROM Sailors
```


## Grouping - GROUP BY
- Split: Partition result relation into groups (According to values of specified attribute)
- Apply: Aggregate some aspects of each group
- Combine: Output 1 tuple per group, with grouping attribute and aggregates

```SQL
SELECT DeptID, AVG(Salary)
FROM Employee
GROUP BY DeptID;
```


## Filtering Groups
- `HAVING` is used to qualify a **GROUP-BY** clause

```SQL
SELECT DeptID, AVG(Salary)
FROM Employee
GROUP BY DeptID
HAVING AVG(Salary) > 3000l
```

![[Pasted image 20260922195831.png]]


## Grouping and NULL
- NULL is **ignored** in **Aggregation**
	- COUNT returns 0 for an empty input multiset
	- All others return NULL for an empty input
- NULL is treated as an **ordinary value** in a **grouped** attribute

![[Pasted image 20260922200139.png]]


## Unique
- Some relations have **multiple candidate** keys: Specify candidate keys with UNIQUE constraints
	- Can only specify multi-column candidate key **after the column** specifications
- Unlike primary keys, **UNIQUE** constrains **DO NOT** exclude **NULL** values
	- This constraint considers **NULL** values to be **unequal**
	- If some attributes in the UNIQUE constraints allow NULLs, DB will **allow multiple rows** with the same values

![[Pasted image 20260922200500.png]]

> [!Note]
> In this case the 2nd Jane Doe will be added since the first NULL and 2nd NULL DO NOT equate each other, it does not violate the constraint and is therefore added.


## Empty set test

Test whether or not a subsquery generates any results at all
- EXISTS (...)
- NOT EXISTS (...)

Find customer with an account but NOT a loan
```SQL
SELECT DISTINCT customer_name FROM depositor d
WHERE NOT EXISTS (
	SELECT * FROM borrower b
	WHERE b.customer_name = d.customer_name
)
```


## Set-Comparison Operators
![[Pasted image 20260922200804.png]]

![[Pasted image 20260922200930.png]]


## CHECK for Constraints
- Used to **constraint** values to **satisfy** some predicate
	- Very effective for constraining columns' domains, and **eliminating** obviously **bad inputs**
	- **MUST** appear **AFTER** the column specification
- Attribute-based: Checked if a tuple gets **new value** via **INSERT** or **UPDATE**
	- Check **new values only**, and old values are unchecked
- Tuple-based: Check **every time** a tuple is **inserted** or **updated**
	- Involves >= 1 attribute of the tuple, must be a tuple-based constraint
	- Will be checked **more frequently** than **attribute-based**
	- Must consider **efficiency** issue in design

> [!Note]
> In theory, can specify any expression that generates a Boolean result
> - This includes nested subqueries
> - In practice, DBMS support for CHECK constraints varies widely, and is often quite limited

![[Pasted image 20260922201413.png]]


## JOIN
![[Pasted image 20260922201428.png]]


## View
- Virtual table defined by a stored **SQL query**
	- **DOES NOT** store data itself
- **Behaves** like a regular table for SELECT queries
	- Can join, filter and aggregate data

### Why use views ?
- **Simplify** complex or repeated queries
- **Restrict access** to specific rows/columns (Security)
- Provide [[W1 DB & Relational Model#Logical Independence|logical data independence]] from schema changes

![[Pasted image 20260922205313.png]]


### Create View Example
Scenario: Expose only sailors rated above 7 to the reporting team
- Querying the view always returns **live**, **up-to-date results**
	- Any change to Sailors instantly reflects in TopSailors

![[Pasted image 20260922205454.png]]


### Writing through a View
- An **UPDATE** through the view **changes the row** in the underlying Sailors table
- A **DELETE** through the view **removes the row** from Sailors **entirely**

![[Pasted image 20260922205639.png]]


# Materialized View

- **Physically stores** the query result, unlike a regular view
	- **Reads are fast** (No need to re-run the underlying query)
	- Data can become **stale** until **explicitly refreshed**
- **MUST** be refreshed to **reflect changes** in the base tables
	- **Manually**, on **schedule** or on commit depending on the database
- Best for **expensive aggregation** that don't need to be **up-to-the-second**
	- Daily sales dashboard, reporting snapshot
- Trade-off: Read speed vs Data freshness

![[Pasted image 20260922211120.png]]


# SQL Functions

- SQL queries can use sophisticated math operations and functions
	- Compute simple functions, aggregates
	- Computer and filter results

- Sometimes, apps require specialized computations
	- Use these in SQL queries
- SQL provide mechanism for defining functions
	- User-Defined Function (UDF)
	- Can be defined in procedural SQL language, or in external language
	- Different vendors provide their own language
		- Oracle: PL/SQL
		- Microsoft: Transact-SQL
		- PostgreSQL: PL/pgSQL
		- MySQL: Stored Procedure
		- Some also support external languages: Java, C, C#, etc

![[Pasted image 20260922211524.png]]

















