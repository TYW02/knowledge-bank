---
title: W5 Relational Algebra & Query Optimization
---

# Communication with DBMS

> [!question] What to Communicate
> - Define the **structure** of database
> 	- CREATE / ALTER / DROP / TRUNCATE / COMMENT / RENAME
> - **Manipulate** data
> 	- SELECT / INSERT / UPDATE / DELETE etc...

> [!question] How to Communicate
> - Structured Query Language (SQL). **Programming-driven**
> - Relational Algebra. **Mathematical-Driven**

## Why Relational Algebra Matters

- **Mathematical foundation** of relational databases and SQL
- Every **serious system** that **stores structured data** (banking, e-commerce, healthcare, social networks) **relies on these principles**
- **Query optimizers** in DBMS use **relational algebra** internally to **transform and speed** up your SQL queries
- Clean, well-structured data is what makes modern AI and data science actually work, relational algebra is a key tool for that structured stage.


# Relational Algebra

- **Procedural language**, SQL is declarative
- Relational algebra ops are like the **machine code** for DMBS
- Relational algebra forms the basis for DBMS implementation
- Many relational databases use relational algebra operations for **representing execution plans**
	- Simple, clean, effective abstraction for **representing how results** will be generated
	- Relatively **easy to manipulate** for **query optimization**


## Relational Algebra Operators
![[Pasted image 20260929190257.png]]

# Fundamental Operator Select

> [!important] Syntax
> Representation: $\sigma_{P}(r)$
> - r: One relation / **table**
> - P: **One or many attributes** of relation r
> 	- Logical Operators: 'AND ^', 'OR V', 'NOT $\lnot$'
> 	- Comparison Operators: >=, >, =, !=, <, <=
> - Return: **All tuples** in r that P **condition is met**

> [!tip] SQL Representation
> ```SQL
> SELECT * 
> FROM r
> WHERE P
> ```

## SELECT Example

![[Pasted image 20260929190726.png]]

> [!question] Find all people from Winterfell
> $\sigma_{\{location = Winterfell\}}(GOT)$
> - Returns tuple 1- 3

> [!question] Find all people from Winterfell and born after year 285
> $\sigma_{\{location=Winterfell \land YOB>285\}}(GOT)$


# Fundamental Operator Project

> [!important] Syntax
> $\prod_{a, b, ...}(r)$

- Project is **column-wise**
- Returned **columns** are from relation r
- Values from the **same domain**
- Possible to **return fewer tuples than the original** relation r

> [!tip] SQL Representation
> ```SQL
> SELECT a, b
> FROM r
> ```

> [!warning] IMPORTANT 
> Project is a **set operation** hence it WILL **NOT return** any **DUPLICATES**
## Project Example

![[Pasted image 20260929191328.png]]

> [!question] Find the name and location of every person
> $\prod_{Name, Location}(GOT)$
> - Returns all 6 tuples, 2 columns

> [!question] Find All Location
> $\prod_{Location}(GOT)$
> - Returns 3 tuples, **NOT 6**
> - Duplicates removed: Project is a **set operation**


# Fundamental Operator Rename

> [!tip] Syntax
> $\rho_{x}(E)$
> - $\rho$: **Rename** operator
> - x: **new name**, User specified
> - E: **Expression**, or the **resulting relation** after certain relational operations
> 
> OR
> 
> If you **want more**: $\rho_{x}(a1, a2, ...)(E)$
> - a1, a2, ...: **Attribute** names can **also be renamed**, if we have the attribute

> [!list] Usage
> - We have a **name to refer** to, if **later working** on the result
> - Resolve **ambiguities**
> - Use in **Cartesian Product**


# Fundamental Operator Set Union

> [!tip] Syntax
> - **Combine**, or union, the **tuples of two relations** r and s: $r \cup s$
> 	- All tuples, BUT **NOT the duplicated ones**
> 
> Requirement: **Same relation schema**
> - Exactly the same, (**Name, type, and order**)

![[Pasted image 20260929192047.png]]

> [!important] Note 
> - In this example we drop the "**Extra**" **duplicate** "Arya Stark"


# Fundamental Operator Set Difference

> [!tip] Syntax
> $r - s$: Fulfil in relation r but NOT in relation s
> - In r BUT NOT IN s
> Requirement
> - Similar as set union, relations have **exactly the same schema**


> [!warning] IMPORTANT
> $A - B$ != $B - A$


![[Pasted image 20260929192354.png]]


# Fundamental Operator Cartesian / Cross Product

> [!tip] Syntax
> **Cross Product**: s x t
> - **Concatenate** the tuples in s and t
> 	- **Keep all attributes** in s and in t. **No abandon**
> - If **SAME attribute name**:
> 	- Add a scope, i.e., `s.id` and `t.id` for the **same attribute** name id
> - Keep ALL tuples
> - Unlike union / difference, **no constraint** for cross
> 


## Cartesian Example

![[Pasted image 20260929192712.png]]

![[Pasted image 20260929192719.png]]



# Natural Join

> [!tip] Syntax
> $s \bowtie t$
> - **Contain all the attributes** of **both tables** but **only one copy of common column**
> 
> Requirement
> - **MUST share** some **columns**, as the reference
> - The **name** and **type** of the columns **must be the same**


![[Pasted image 20260929192959.png]]

 >[!question] Who is both Stark and Targaryen ?
 >$\prod_{Name}(s \bowtie t)$
 >
 >OR
 >
 >$\prod_{Name}(\sigma_{s.Name=t.Name}(s x t))$


# Outer Join

- Natural join require the perfect match, if **retain some imperfect ones** (Use outer join)
- If imperfect ones allowed, what to do with missing values ?
	- use `NULL`
- Similar to set difference, **direction matters**

> [!important] Left Outer Join
> 
![[Pasted image 20260929193406.png]]

> [!important] Right Outer Join
> ![[Pasted image 20260929193425.png]]

> [!important] Full Outer Join
> ![[Pasted image 20260929193439.png]]


# Assignment

> [!tip] Syntax
> temp <- E
> - Stores the **result of expression** E in a temporary relation named `temp`
> - `temp` can be **used in later expressions**
> - **Splits** a long query into **readable steps**

> [!question] Example: Who from Winterfell was born after 285 ?
> - temp1 <- $\sigma_{Location=Winterfell}(GOT)$
> - temp2 <- $\sigma_{YOB>285}(temp1)$
> - result <- $\prod_{Name}(temp2)$
> - Return Arya Stark


# Query Optimization

> [!important] Motivation
> - Same query can run in **milliseconds or minutes** depending on how it's **written and indexed**
> - **Optimization** matters for cost, scalability, and user experience, especially with **large datasets**

> [!bug] Factors Affecting Performance
> - Data Volume, Query Complexity, Hardware Capabilities

> [!question] Optimization Goals
> Reducing **execution** and **response time**, **minimizing resource consumption**, and improving **scalability** and **transaction** throughput

> [!watch] Monitor
> Execution Plan: Step-by-step strategy outline how the database will process the query

![[Pasted image 20260929194138.png]]

> [!note] NOTE
> On the **left** we **JOIN** both table **first** before **FILTERing**, this makes it **slower** since we are now **increasing the search space** BEFORE filtering.
> 
> On the right because we **filter** the country **first** we get all **SMALLER** table **BEFORE** joining .



## Optimize Select: SELECT only Needed Columns

> The optimizer can't fix everything: Write queries that give it less work

- Use **SELECT** instead of **SELECT *** (Projection pushdown)
```SQL
SELECT customer_id, customer_name, email
FROM customers;
```

- Avoid **removing duplication** if it is not important
```SQL
SELECT Distinct -> SELECT
UNION -> UNION ALL
```

- Keep Wild Cards at the End of Phrase
```SQL
SELECT name, salary FROM Employee WHERE name LIKE "%Ram%"
SELECT name, salary FROM Employee WHERE name LIKE "Ram%"
```

> [!note] NOTE
> Here, since we have the **wildcard** at the **start** this means that **anything** can be **in front of Ram** which will take a **long time to search for.**


## Filter Early with WHERE

### Works
```SQL
SELECT customer_id, SUM(total_amount)
FROM Orders
GROUP BY customer_id
HAVING customer_id > 100;
```


### Better
```SQL
SELECT customer_id, SUM(total_amount)
FROM Orders
WHERE customer_id > 100
GROUP BY customer_id;
```

> [!note] Why do this ?
> - **WHERE** filters rows **before** grouping/aggregation, **HAVING** filters after
> - Filtering **earlier reduces** the amount of **data processed**.


## Use Exist() instead of Count()

### Find all customers that placed at least one order

```SQL
SELECT customer_id
FROM customers
WHERE (SELECT COUNT(*) FROM orders WHERE orders.customer_id = customers.customer_id) > 0;
```

```SQL
SELECT customer_id
FROM customers
WHERE EXISTS(SELECT 1 FROM orders WHERE orders.customer_id = customers.customer_id);
```

> [!tip] NOTE
> - `Exists()` will run till it finds the **first matching entry** whereas
> - `Count()` will keep on running and **provide all the matching records**


## Subquery Optimization: Rewrite Correlated Subqueries

### Find the total order amount for each customer

```SQL
SELECT customer_id, (SELECT SUM(order_amount) FROM orders WHERE orders.customer_id = customers.customer_id) AS total_sales
FROM customers;
```

> Iterates **over each customer** and **executes a subquery** to calculate their total sales: **Inefficient for LARGE** datasets.

```SQL
SELECT customers.customer_id, SUM(orders.order_amount) AS total_sales
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id
GROUP BY customers.customer_id
```

> JOIN -> GROUP BY -> SUM (Single Pass, Faster)


## Join Optimization

> Select the JOIN type that aligns with the data you want to retrieve

```SQL
SELECT * FROM orders, customers;
-- Not efficient, will join everything
```

```SQL
SELECT orders.order_id, customers.customer_name
FROM orders INNER JOIN customers
ON orders.customer_id = customers.customer_id;
```


# Use Indexes Effectively

![[Pasted image 20260929195742.png]]


# Patterns that break Index Usage
![[Pasted image 20260929195806.png]]

# Checking the Execution Plan
![[Pasted image 20260929195821.png]]


## Checklist
- [ ] Am I selecting **only needed** columns ?
- [ ] Am I **filtering as early as possible** with WHERE ?
- [ ] Are my **WHERE/JOIN/ORDER BY** columns **indexed appropriately** ?
- [ ] Am I **avoiding functions/calculations** on **indexed columns** ?
- [ ] Are my **joins necessary and efficient** (no unnecessary OUTER JOINs) ?
- [ ] Have I **checked the execution plan** ?
- [ ] Are **statistics** and **indexes up to date** ?










