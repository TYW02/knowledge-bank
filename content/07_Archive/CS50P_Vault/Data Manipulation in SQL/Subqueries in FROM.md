Tags: #Subqueries 



# Subqueries in FROM
- Restructure and transform your data
	- Transforming data from long and wide before selecting
	- Prefiltering data
- Calculating *aggregates* of aggregates
	- Which 3 teams has the highest average of home goals scored ?
		1. Calculate the ```AVG``` for each team
		2. Get the 3 highest of the ```AVG``` values


## FROM subqueries
```mysql
SELECT 
	t.team_long AS team,
	AVG(m.home_goal) AS home_avg
FROM match AS m
LEFT JOIN team AS t
ON m.hometeam_id = t.team_api_id
WHERE season = '2011/2012'
GROUP BY team;
```

1. Create the query that will become your subquery
	- This query here selects the team's long name from the team table, and the AVG of home_goal column from the match table
2. The team table is left joined onto the match table using hometeam_id which will give you identity of the home team.
3. The query is then filtered by season and grouped by team.


## ... to main queries !
```mysql
FROM (SELECT 
			 t.team_long_name AS team,
			 AVG(m.home_goal) AS home_avg
		 FROM match AS m
		 LEFT JOIN team AS t
		 ON m.hometeam_id = t.team_api_id
		 WHERE season = '2011/2012'
		 GROUP BY team) AS subquery
```





```mysql
SELECT team, home_avg
FROM (SELECT 
			 t.team_long_name AS team,
			 AVG(m.home_goal) AS home_avg
		 FROM match AS m
		 LEFT JOIN team AS t
		 ON m.hometeam_id = t.team_api_id
		 WHERE season = '2011/2012'
		 GROUP BY team) AS subquery
ORDER BY home_avg DESC
LIMIT 3;
```




# Things to remember
- You can create multiple subqueries in one FROM statement
	- Alias them !
	- Join them !
- You can join a subquery to a table in FROM
	- Include a joining columns in both tables !






































