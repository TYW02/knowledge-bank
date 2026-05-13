

# Nested Subqueries ?
- Subquery inside another subquery
- Perform multiple layers of transformation


# A Subquery...
- How much did each country's average differ from the overall average ?
```mysql
SELECT 
	c.name AS country
	AVG(m.home_goal + m.away_goal) AS avg_goals,
	AVG(m.home_goal + m.away_goal) -
		(SELECT AVG(home_goal + away_goal)
		FROM match) AS avg_diff
FROM country AS c
LEFT JOIN match AS m
ON c.id = m.country_id
GROUP BY country;
```


# ...inside a subquery !
- How does each month's total goals differ from the average monthly total of goals scored ?
```mysql
SELECT
	EXTRACT(MONTH FROM date) AS month,
	SUM(m.home_goal + m.away_goal) AS total_goals,
	SUM(m.home_goal + m.away_goal) -
	(SELECT AVG(goals)
	FROM (SELECT
			EXTRACT(MONTH FROM date) AS month,
			SUM(home_goal + away_goal) AS goals
			FROM match
			GROUP BY month)) AS avg_diff
FROM match AS m
GROUP BY month;
```


## Inner subquery
```mysql
SELECT
	EXTRACT(MONTH FROM date) AS month,
	SUM(home_goal + away_goal) AS goals
FROM match
GROUP BY month;
```
1. Select the sum of goals scored in each month.
	- The month is queried using the EXTRACT function, FROM the date.


## Outer subquery
```mysql
SELECT AVG(goals)
FROM (SELECT
	 EXTRACT(MONTH FROM date) AS month,
	 AVG(home_goal + away_goal) AS goals
FROM match
GROUP BY month) AS s;
```
Calculate an average of the values generared in the previous table, giving you the average monthly goals scored.
Since this result is a scalar subquery, you can now place it in the main query for calculating the final data set.



## Final Query
```mysql
SELECT
	EXTRACT(MONTH FROM date) AS month,
	SUM(m.home_goal + m.away_goal) AS total_goals,
	SUM(m.home_goal + m.away_goal) -
	(SELECT AVG(goals)
	FROM (SELECT
			EXTRACT(MONTH FROM date) AS month,
			SUM(home_goal + away_goal) AS goals
			FROM match
			GROUP BY month)) AS avg_diff
FROM match AS m
GROUP BY month;
```



# Correlated nested subqueries
- Nested subqueries can be correlated or uncorrelated 
	- Or ... a combination of the two
	- Can reference information from the outer subquery or main query


- What is each country's average goals scored in the 2011/2012 season ?
```mysql
SELECT 
	c.name AS country,
	(SELECT AVG(home_goal + away_goal)
	FROM match AS m
	WHERE m.country_id = c.id
		AND id IN (
				SELECT id
				FROM match
				WHERE season = '2011/2012')) AS avg_goals
FROM country AS c
GROUP BY country;
```






































