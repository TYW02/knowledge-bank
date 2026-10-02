# Joins
> [!question] Joins
> **(Lec3 — Joins, applied)**  
> Write a SQL query using `INNER JOIN` syntax to retrieve all customer names and their order dates, given tables `customers(customer_id, customer_name)` and `orders(order_id, customer_id, order_date)`.
> 
> [[Joins#INNER JOIN|Answer]]

> [!question] Given `Products(pid, name, price, category)`, write a query to find products priced above the average price within their own category
> > [!Answer]-
> > ```SQL
> > SELECT p1.name
> > FROM Products p1
> > WHERE p1.price > (
> > 	SELECT AVG(p2.price)
> > 	FROM Products p2
> > 	WHERE p2.category = p1.category
> > );
> > ```
> > - For each product `p1`, the subquery recalculate the avg price ONLY among products in p1's own category
# Union
> [!Union]
> What happens when the UNION operator is used without the ALL keyword ?
> 
> [[Union#Without ALL|Union]]

> [!Union vs Union ALL]
> How is UNION different from UNION ALL ?
> 
> [[Union#Union vs Union ALL|Answer]]

# View
> [!View]
> What happens when a View is created using the WITH CHECK OPTION ?
> 
> [[View]]

> [!View VS Table]
> How is a View different from a Table ?
> 
> [[View#View VS Table|Answer]]

> [!Multiple Table]
> What happens if you try to update a View that involves multiple tables or complex aggregations ? 
> 
> [[View#Multiple table updates|Updates]]

# Materialised View
> [!Trade-off]
> What is the primary trade-off when deciding to use a Materialised View ?
> 
> [[Materialised View#Primary Trade-off|Primary Trade-off]]

# NULL
> [!NULL]
> What happens when a UNIQUE constraint is placed on a column that allows NULL values ? 
> 
> [[NULL#Unique Constraint with NULL Values|NULL]]

# Group By
> [!Group By]
> What happens to NULL values when the GROUP BY clause is executed ?
> 
> [[Group By#NULL values GROUP BY|NULL with Group By]]

# ANY
> [!Any vs ALL]
> How is the ANY operator different from the ALL operator in set comparison ?
> 
> [[Any#Any vs All| Answer]]

# Order By
> [!Order By]
> When using ORDER BY with multiple attributes, how is the sort priority determined ?
> 
> [[Order By#Sort Priority|Sort Priority]]


# Check
> [!Check]
> What is a primary efficiency concern when using tuple-based CHECK constraints ?
> 
> [[Check#Primary Efficiency Concern|Concern]]

# Count
> [!Count]
> Which aggregate function returns the total count of rows, including those with NULL values ?
> 
> [[COUNT#Count including NULL|COUNT]]

> [!question] Given `employee(ssn, name, salary, dept_name)`, write a query to find the names of employees earning more than the average salary of all employees.
> > [!Answer]-
> > ```SQL
> > SELECT name FROM employee WHERE > (SELECT AVG(salary) FROM employee);
> > ```
> > - Aggregate functions **can't be mixed** with **row-level filtering** in the **SAME scope**.
> > - You need a **nested SELECT** to **compute the aggregate first**, then compare against it.

# Exists
> [!question] Given `Boats(bid, bname, color)` and `Reserves(sid, bid, day)`, write a query using `EXISTS` to find boat names that have never been reserved.
> > [!Answer]-
> > ```SQL
> > SELECT bname FROM Boats b
> > WHERE NOT EXISTS (
> > 	SELECT * FROM Reserves r WHERE r.bid = b.bid
> > )
> > ```
> > - Return each boat where no reservation row matches its bid
> > - `EXISTS / NOT EXISTS` always take a **complete subquery** in parentheses as their argument.



















