

# Correlated Subquery
- Uses values from the *outer* query to generate a resu;t
- Re-run for every row generated in the final data set
- Used for advanced joining, filtering, and avaluating data


## A Simple Example
- Which match stages tend to have a higher than average number of goals scored ?
```mysql
SELECT 
	s.stage,
	ROUND(s.avg_goals,2) AS avg_goal,
	(SELECT AVG(home_goal + away_goal) FROM match
	WHERE season = '2012/2013') AS overall_avg
FROM
	(SELECT 
		stage,
		AVG(home_goal + away_goal) AS avg_goals
		FROM match
		WHERE season = '2012/2013'
		GROUP BY stage) AS s
WHERE s.avg_goals > (SELECT AVG(home_goals + away_goals)
					FROM match
					WHERE season = '2012/2013');
```

You achieve this using 3 simple subqueries in the SELECT, FROM and WHERE statements.
	

# A Correlated example
```mysql
SELECT 
	s.stage,
	ROUND(s.avg_goals,2) AS avg_goal,
	(SELECT AVG(home_goal + away_goal) FROM match
	WHERE season = '2012/2013') AS overall_avg
FROM
	(SELECT 
		stage,
		AVG(home_goal + away_goal) AS avg_goals
		FROM match
		WHERE season = '2012/2013'
		GROUP BY stage) AS s
WHERE s.avg_goals > (SELECT AVG(home_goals + away_goals)
					FROM match
					WHERE s.stage > m.stage);
```


However, the same output can also be produced with a correlated subquery.
	(Let's focus on the subquery in the WHERE statement.)
		Instead of including a filter by season, the WHERE clause filters for data where the outer table's match stage, pulled from the subquery in FROM, is HIGHER than the overall average generated in the WHERE subquery.
			- "Return stages where the values in the subquery are higher than the average"



# Simple vs Correlated Subqueries
| Simple Subquery                                  | Correlated Subquery                        |
| ------------------------------------------------ | ------------------------------------------ |
| - Can be run *independently* from the main query | - *Dependent* on the main query to execute |
| - Evaluated once in the whole query              | - Evaluated in loops <br/> - Significantly slows down query runtime                                           |



# Correlated Subqueries
- What is the average number of goals scored in each country ?
```mysql
SELECT 
	c.name AS country
	AVG(m.home_goal + m.away_goal)
		AS avg_goals
FROM country AS c
LEFT JOIN match AS m
ON c.id = m.country_id
GROUP BY country;
```


## Another way to do it
```mysql
SELECT 
	c.name AS country
	(SELECT
		AVG(m.home_goal + m.away_goal)
			AS avg_goals
		FROM country AS c
		WHERE m.country_id = c.id)
			AS avg_goals
FROM country AS c
GROUP BY country;
```
























