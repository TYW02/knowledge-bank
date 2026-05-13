Tags: #Subqueries 



# SELECTing what ?
- Returns a Single Value
	- Include aggregate values to compare to individual values
- Used in mathematical Calculations
	- Deviation from the average



# Subqueries in SELECT
```mysql
SELECT
	season,
	COUNT(id) AS matches,
	(SELECT COUNT(ID) FROM match) AS total_matches
FROM match
GROUP BY season;
```
| Season    | matches | total_matches |
| --------- | ------- | ------------- |
| 2011/2012 | 3220    | 12837         |
| 2012/2013 | 3260    | 12837         |
| 2013/2014 | 3032    | 12837         |
| 2014/2015 | 3325    | 12837              |



## SELECT subqueries for mathematical calculations

```mysql
SELECT AVG(home_goal + away_goal)
FROM match
WHERE season = '2011/2012';
```


```mysql
SELECT
	date,
	(home_goal + away_goal) AS goals,
	(home_goal + away_goal) - 2.72 AS diff
FROM match
WHERE season = '2011/2012';
```



# Subqueries in SELECT
```mysql
SELECT 
	date,
	(home_goal + away_goal) AS goals,
	(home_goal + away_goal) - 
		(SELECT AVG(home_goal + away_goal)
		FROM match
		WHERE season = '2011/2012') AS diff
FROM match
WHERE season = '2011/2012';
```
You can use a subquery that calculates a value for you in your SELECT statement, and subtract it from the total goals in that match.




# SELECT subqueries -- things to keep in mind
- Need to return a SINGLE value
	- Will generate an error otherwise
- Make sure you have all filters in right places
	- Properly filter both the main and the subquery !
```mysql
SELECT
	date,
	(home_goal + away_goal) AS goals,
	(home_goal + away_goal) - 
		(SELECT AVG(home_goal + away_goal)
		FROM match
		WHERE season = '2011/2012') AS diff
FROM match
WHERE season = '2011/2012';
```













































