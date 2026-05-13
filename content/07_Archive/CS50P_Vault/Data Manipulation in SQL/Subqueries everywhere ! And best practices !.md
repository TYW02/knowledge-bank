Tags: #Subqueries 



# As many subqueries as you want ...
- Can include multiple subqueries in SELECT, FROM, WHERE
![[Pasted image 20230106153908.png]]


# Format your queries
- Line up SELECT, FROM, WHERE, and GROUP BY
```mysql
SELECT
	col1,
	col2,
	col3
FROM table1
WHERE col1 = 2;
```




# Annotate your queries
```mysql
/* This query filters for col1 = 2
and only selects data from table1 */
SELECT
	col1,
	col2,
	col3
FROM table1
WHERE col1 = 2;
```

```mysql
SELECT
	col1,
	col2,
	col3
FROM table1 -- this table has 10,000 rows
WHERE col1 = 2; -- Filter WHERE value 2
```



# Indent your queries
- Indent your subqueries
```mysql
SELECT 
	col1,
	col2,
	col3
FROM table1
WHERE col1 IN 
		(SELECT id
		FROM table2
		WHERE year = 1991);
```

![[Pasted image 20230106154329.png]]



# Is that subquery necesssary ?
- Subqueries require computing power
	- How big is your database ?
	- How big is the table you're querying from ?
- Is the subquery actually necessary ?



# Properly filter each subquery!
- Watch your filters !
![[Pasted image 20230106154614.png]]
When constructing a main query with multiple subquery, make sure that your filters are properly placed in every subquery, and the main query, in order to generate accurate results.





















