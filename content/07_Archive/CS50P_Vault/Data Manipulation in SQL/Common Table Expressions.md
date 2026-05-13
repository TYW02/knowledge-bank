
# When adding subqueries...
- Query complexity increases quickly !
	- Information can be difficult to keep track of



# Common Table Expressions

## Common Table Expressions (CTEs)
- Table *declared* before the main query
- *Named* and *referenced* later in FROM statement


### Setting up CTEs
```mysql
WITH cte AS (
	SELECT col1, col2
	FROM table)
SELECT 
	AVG(col1) AS avg_col
FROM cte;
```
- Instead of wrapping subqueries inside, say the FROM statement, you name it using the WITH statement, and then reference it by name later in the FROM statement as if it were any other table in your database.



# Take a subquery in FROM
```mysql
SELECT
	c.name AS country,
	COUNT(s.id) AS matches
FROM country AS c
INNER JOIN(
	SELECT country_id, id
	FROM match
	WHERE (home_goal + away_goal) >= 10) AS s
ON c.id = s.country_id
GROUP BY country;
```
FROM statement --> Generate a list of country id's and match id that meet a certain criteria
Subquery is then joined to the country table and the number of matches in the subquery is counted in the main query.


# Place it at the beginning
```mysql
WITH s AS (
	SELECT country_id, id
	FROM match
	WHERE (home_goal + away_goal) >= 10
)
```
- In order to rewrite this query using a common table expression to represent the subquery, simply take the subquery out of the FROM clause, place it at the beginning of your query.

- Declare it using the syntax WITH, followed by a CTE name, and AS. So, here we're starting our CTE, s, by stating WITH s AS, and then placing the subquery inside parentheses. It's now a common table expression!



# Show me the CTE
```mysql
WITH s AS (
	SELECT country_id, id
	FROM match
	WHERE (home_goal + away_goal) >= 10
)
SELECT
	c.name AS country,
	COUNT(s.id) AS matches
FROM country AS c
INNER JOIN s
ON c.id = s.country_id
GROUP BY country;
```


```mysql
WITH s1 AS (
	SELECT country_id, id
	FROM match
	WHERE (home_goal + away_goal) >= 10),
s2 AS (
	SELECT country_id, id
	FROM match
	WHERE (home_goal + away_goal) <=1
)
SELECT
	c.name AS country,
	COUNT(s1.id) AS high_scores,
	COUNT(s2.id) AS low_scores,
FROM country AS C
INNER JOIN s1
ON c.id = s1.country_id
INNER JOIN s2
ON c.id = s2.country_id
GROUP BY country;
```
- If you have multiple subqueries that you want to turn into a common table expression, you can simply list them one after another, with a comma in between each CTE, and NO comma after the last one. 
- You can then retrieve the information you need into the main query -- just make sure you properly join this second CTE as well!



# Why use CTEs ?
- Executed once
	- CTE is then stored in memory
	- Improves query performance
- Improving organization of queries
- Referencing other CTEs
- Referencing itself(SELF JOIN)





























