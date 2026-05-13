


# Working with aggregate values
- Requires you to use GROUP BY with all non-aggregate columns
```mysql
SELECT
	country_id,
	season,
	date,
	AVG(home_goal) AS avg_home
FROM match
GROUP BY country_id;
```

>[!INFO]
>	ERROR: column "match.season" must appear in the GROUP BY clause or be used in an aggregate function.



# Introducing Window Functions!
- Perform calculations on an already generated result set (a window)
- Aggregate calculations
	- Similar to subqueries in SELCT
	- Running totals, rankings, moving average


# What's a window function ?
- How many goals were scored in each match in 2011/2012, and how did that compare to the average ?
```mysql
SELECT 
	date,
	(home_goal + away_goal) AS goals,
	(SELECT AVG(home_goal + away_goal)
		FROM match
		WHERE season = '2011/2012') AS overall_avg
FROM match
WHERE season = '2011/2012'
```


```mysql
SELECT
	date,
	(home_goal + away_goal) AS goals,
	AVG((home_goal + away_goal) OVER() AS overall_avg
FROM match
WHERE season = '2011/2012'
```



# Generate a RANK
- What is the rank of matches based on number of goals scored ?
```mysql
SELECT
	date,
	(home_goal + away_goal) AS goals
FROM match
WHERE season = '2011/2012'
```
- A RANK simply creates a column numbering your data set from highest to lowest, or lowest to highest, based on a column that you specify.


```mysql
SELECT
	date.
	(home_goal + away_goal) AS goals,
	RANK() OVER(ORDER BY home_goal + away_goal) AS goals_rank
FROM match
WHERE season = '2011/2012'
```
- To create the rank, you start with the RANK function, using parentheses, followed by the OVER clause. 
- Inside the OVER clause, include the ORDER BY clause, and the column or columns you want to use to generate the rank. 
- By default, the RANK function orders the results and ranking from smallest to largest values.




```mysql
SELECT
	date.
	(home_goal + away_goal) AS goals,
	RANK() OVER(ORDER BY home_goal + away_goal DESC) AS goals_rank
FROM match
WHERE season = '2011/2012'
```
- By adding the DESC function to reverse the order of the rank, just as you would if you were using ORDER BY at the end of your query. 
- You'll notice that the RANK function automatically ties identical values, such as the first 2 results, and then skips the next value in the rank.


# Key Differences
- Processed *after* every part of query except ORDER BY 
	- Uses information in result set rather than database
- Available in PostgreSQL, Oracle, MySQL, SQL Server...
	- but NOT SQLite

























