Tags: #CASE 


# In CASE you need to aggregate
- ==CASE== statements are great for 
	- Categorizing data
	- Filtering data
	- Aggregating data


# COUNTing CASES
- How many home and away goals did Liverpool score in each season ?
| season    | home_wins | away_wins |
| --------- | --------- | --------- |
| 2011/2012 |           |           |
| 2012/2013 |           |           |
| 2013/2014 |           |           |
| 2014/2015          |           |           |


## CASE WHEN with COUNT
```mysql
SELECT
	season,
	COUNT(CASE WHEN hometeam_id = 8650
				AND home_goal > away_goal
				THEN id END) AS home_wins
FROM match
GROUP BY season;
```
- WHEN clause logic
	- Did Liverpool play as the home team ? AND did home team score higher than away team ?
	- The difference begins in THEN clause
		- Instead of returning string, you return the id.
		- When this CASE statement is inside the COUNT function, it COUNTS every id returned by CASE statement.


### Enhanced Version
```mysql
SELECT
	season,
	COUNT(CASE WHEN hometeam_id = 8650 AND home_goal > away_goal THEN id END) AS home_wins,
	COUNT(CASE WHEN awayteam_id = 8650 AND away_goal > home_goal THEN id END) AS away_wins
FROM match
GROUP BY season;
```
| season    | home_wins | away_wins |
| --------- | --------- | --------- |
| 2011/2012 | 6         | 8         |
| 2012/2013 | 9         | 7         |
| 2013/2014 | 16        | 10        |
| 2014/2015 | 10        | 8         |

- Add a 2nd CASE statement for the away team, and group the quey by the season. 
- When counting information in a CASE statement, you can return anything you'd like
	- Number
	- Text
	- Columns


# CASE WHEN with SUM
```mysql
SELECT
	season,
	SUM(CASE WHEN hometeam_id = 8650
			THEN home_goal END) AS home_goals,
	SUM(CASE WHEN awayteam_id = 8650
				THEN away_goal END) AS away_goals
FROM match
GROUP BY season;
```

| season    | home_goal | away_goal |
| --------- | --------- | --------- |
| 2011/2012 | 24        | 23        |
| 2012/2013 | 33        | 38        |
| 2013/2014 | 53        | 48        |
| 2014/2015 | 30        | 22          |

- If the hometeam_id is Liverpool's, return the home_goal value.
- The ELSE condition is assumed to be NULL, so the query returns the total home_goals scored by Liverpool in each season.


# The CASE is fairly AVG...
```mysql
SELECT
	season,
	AVG(CASE WHEN hometeam_id = 8650
			THEN home_goal END) AS avg_homegoals,
	AVG(CASE WHEN awayteam_id = 8650
				THEN away_goal END) AS avg_awaygoals
FROM match
GROUP BY season;
```
| season    | avg_homegoals | avg_awaygoals |
| --------- | ------------- | ------------- |
| 2011/2012 | 1.269423942   | 1.2105274973  |
| 2012/2013 | 1.73603284023 | 2             |
| 2013/2014 | 2.78941231    | 2.52633423    |
| 2014/2015 | 1.578943294   | 1.15789234    |

- The AVG function with CASE:
	- You can calculate an average of data. 
		- You can do this using CASE in the EXACT same way you used the SUM function.
		- Just change SUM for AVG


# A ROUNDed AVG

#### Example
```mysql
ROUND(3.14159324234, 2)
3.14
```


```mysql
SELECT
	season,
	ROUND(AVG(CASE WHEN hometeam_id = 8650
			THEN home_goal END), 2) AS avg_homegoals,
	ROUND(AVG(CASE WHEN awayteam_id = 8650
			THEN away_goal END), 2) AS avg_home_goals
FROM match
GROUP BY season;
```

| season    | avg_homegoals | avg_awaygoals |
| --------- | ------------- | ------------- |
| 2011/2012 | 1.26          | 1.21          |
| 2012/2013 | 1.73          | 2             |
| 2013/2014 | 2.78          | 2.52          |
| 2014/2015 | 1.57          | 1.15          |


# Percentages with CASE and AVG
```mysql
SELECT 
	season,
	ROUND(AVG(CASE WHEN hometeam_id = 8455 AND home_goal > away_goal THEN 1 WHEN
	hometeam_id = 8455 AND home_goal < away_goal THEN 0 END), 2) AS pct_homewins,
	ROUND(AVG(CASE WHEN awayteam_id = 8455 AND away_goal > home_goal THEN 1 WHEN
	awayteam_id = 8455 AND away_goal < home_goal THEN 0 END), 2) AS pct_awaywins
FROM match
GROUP BY season;
```

| season    | pct_homewins | pct_awaywins |
| --------- | ------------ | ------------ |
| 2011/2012 | 0.75         | 0.5          |
| 2012/2013 | 0.86         | 0.67         |
| 2013/2014 | 0.94         | 0.67         |
| 2014/2015 | 1            | 0.79             |


- The question we're answering here is, "What percentage of Liverpool's games did they win in each season ?"
	- The first component of this CASE statement is a WHEN clause identifying what you're calculating a percentage of games won.















