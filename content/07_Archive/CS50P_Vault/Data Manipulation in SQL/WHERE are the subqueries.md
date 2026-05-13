Tags: #Subqueries


# What is a subquery ?
- A query *nested* inside another query
```mysql
SELECT column
FROM (SELECT column
	 FROM table) AS subquery;
```

- Useful for intermediary transformations

Often in order to retrieve information you want, you have to perform some intermediary transformations to your data before selecting, filtering, or calculating informaiton.


# What do you do with subqueries ?
- Can be in *any* part of a query
	- ==SELECT===, ==FROM==, ==WHERE==, ==GROUP BY ==

- Can return a variety of information
	- Scalar quantities (3.14159, -2, 0.0001)
	- A list (id = (12, 25, 392, 401, 939))
	- A table



# Why subqueries ?
- Comparing groups to summarized values
	- How did Liverpool compare to the English Premier League's average performance for that year ?

- Reshaping data
	- What is the highest monthly average of goals scored in the Bundesliga ?

- Comparing data that cannot be joined
	- How do you get both the home and away team names into a table of match results ?



# Simple Subqueries
- Can be evaluated independently from the outer query
```mysql
SELECT home_goal
FROM match
WHERE home_goal > (
	SELECT AVG(home_goal)
	FROM match);
SELECT AVG(home_goal) FROM match;
```
The example you see here has a subquery in the WHERE clause -- if you copy the entire inner query, "SELECT the average home goal FROM the match table", you cqn run it on its own and get a result.


- Is only processed once in the entire statement
```mysql
SELECT home_goal
FROM match
WHERE home_goal > (
	SELECT AVG(home_goal)
	FROM match
);
```
A simple subquery is also evaluated once in the entire query.
	1. This means that SQL first processes the information inside the subquery, gets the information it needs, and then moves on to processing information in the OUTER query.
		2. The subquery in WHERE is processed first, generating the overall average of home goals scored.
			3. SQL then moved onto the main query, treating the subquery like the single, aggregate value it just generated



# Subqueries in the WHERE clause
- Which matches in the 2012/2013 season scored home goals higher than overall average ?
```mysql
SELECT date, hometeam_id, awayteam_id, home_goal, away_goal
FROM match
WHERE season = '2012/2013'
	AND home_goal > (SELECT AVG(home_goal)
					FROM match);
```
| date       | hometeam_id | awayteam_id | home_goal | away_goal |
| ---------- | ----------- | ----------- | --------- | --------- |
| 2012-07-28 | 9988        | 1773        | 5         | 2         |
| 2012-07-29 | 9987        | 9984        | 3         | 3         |
| 2012-10-05 | 9993        | 9991        | 2         | 2          |

Very useful for filtering results based on information you'd have to calculate separately beforehand.
For example:
	You could calculate the average, and then include that number in the main query...
	OR
	You could put the query directly into the WHERE clause, inside parentheses. This way, you have one less manual step to perform before getting the results you need.


# Subquery filtering list with IN
- Which teams are part of the Poland's league ?
```mysql
SELECT
	team_long_name,
	team_short_name AS abbr
FROM team
WHERE
	team_api_id IN 
	(SELECT hometeam_id
	FROM match
	WHERE country_id = 15722);
```
Subqueries are also useful for generating a filtering list.
For example:
"Which teams are part of Poland's league ?"
The "team table" doesn;t have the country IDs, but the "match" table has both country and team IDs.
By querying a list of hometeam_id's from match where the country_id is 15722, which indicates "Poland", you can generate a list to compare to the team_api_id column IN the WHERE clause.



















