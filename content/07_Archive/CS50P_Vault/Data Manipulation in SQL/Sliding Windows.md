

# Sliding Windows
- Perform Calculations relative to the current row
- Can be used to calculate running totals, sums, average, etc
- Can be partitioned by one or more columns


# Sliding Window Keywords
```mysql
ROWS BETWEEN <start> AND <finish>

PRECEDING
FOLLOWING
UNBOUNDED PRECEDING
UNBOUNDED FOLLOWING
CURRENT ROWS
```



# Sliding Window Example
```mysql
-- Manchester City Home Games
SELECT
	date,
	home_goal,
	away_goal,
	SUM(home_goal)
		OVER(ORDER BY date ROWS BETWEEN
			UNBOUNDED PRECEDING AND CURRENT ROWS) AS running_total
FROM match
WHERE hometeam_id = 8456 AND season = '2011/2012'
```
- PRECEDING and FOLLOWING are used to specify the number of rows before, or after, the current row that you want to include in a calculation. 
- UNBOUNDED PRECEDING and UNBOUNDED FOLLOWING tell SQL that you want to include every row since the beginning, or the end, of the data set in your calculations. 
- Finally, CURRENT ROW tells SQL that you want to stop your calculation at the current row.


# Sliding Window Frame
```mysql
-- Manchester City Home Games
SELECT
	date,
	home_goal,
	away_goal,
	SUM(home_goal)
		OVER(ORDER BY date
		ROWS BETWEEN 1 PRECEDING
		AND CURRENT ROWS) AS last2
FROM match
WHERE hometeam_id = 8456
	AND season = '2011/2012';
```



























