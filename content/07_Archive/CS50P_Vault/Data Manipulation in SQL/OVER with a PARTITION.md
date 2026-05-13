

# OVER and PARTITION BY
- Calculate separate values for different categories
- Calculate *different* calculations in the same column
```mysql
AVG(home_goal) OVER(PARTITION BY season)
```
- A partition allows you to calculate separate values for different categories established in a partition.



# Partition your data
- How many goals were scored in each match, and how did that compare to the overall average ?
```mysql
SELECT
	date,
	(home_goal + away_goal) AS goals,
	AVG(home_goals + away_goals) OVER() AS overall_avg
FROM match;
```



- How many goals were scored in each match, and how did that compare to the season's average?
```mysql
SELECT
	date,
	(home_goal + away_goal) AS goals,
	AVG(home_goal + away_goal) OVER(PARTITION BY season) AS season_avg
FROM match;
```
- Specifying, "PARTITION BY season" returns each season's average on each row, in accordance to the season that each record belongs to. 
- As you can see, rows 1 and 2 are matches played in the 2011/2012 season, and the season_avg column contains the 2011/2012 season average. 
- Rows 3 and 4 are part of the 2012/2013 season, and return the 2012/2013 season average.



# PARTITION by Multiple Columns
```mysql
SELECT
	c.name,
	m.season,
	(home_goal + away_goal) AS goals,
	AVG(home_goal + away_goal)
		OVER(PARTITION BY m.season, c.name) AS season_ctry_avg
FROM country AS c
LEFT JOIN match AS m
ON c.id = m.country_id
```
- The OVER clause contains two columns to partition the AVG goals scored--season, and country. 
- The result set returns the average goals scored broken out by season and country. 
	- In row 1, a match was played in Belgium in the 2011/2012 season, and had 1 goal scored throughout the match. This is compared to the 2.88, which is the average goals scored in Belgium in the 2011/2012 season.



# PARTITION BY considerations
- Can partition data by 1 or more columns
- Can partition aggregate calculations, rank, etc


















