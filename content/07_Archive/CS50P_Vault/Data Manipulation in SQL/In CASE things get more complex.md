Tags: #CASE

# Reviewing CASE WHEN


## Summary
```mysql
SELECT
	date,
	season,
	CASE WHEN home_goal > away_goal THEN 'Home Team Win!'
		WHEN home_goal < away_goal THEN 'Away Team Win!'
		ELSE 'Tie' END AS outcome
FROM match;
```


# CASE WHEN ... AND then some
- Add multiply logical conditions to your ==WHEN== clause!
```mysql
SELECT date, hometeam_id, awayteam_id,
	CASE WHEN hometeam_id = 8455 AND home_goal > away_goal
		THEN 'Chelsea home win!'
	WHEN awayteam_id = 8455 AND home_goal < away_goal
		THEN 'Chelsea away win!'
	ELSE 'Loss or tie :(' END AS outcome
FROM match
WHERE hometeam_id = 8455 OR awayteam_id = 8455;
```

- If you want to test multiple logical conditions in a CASE statement, you can use AND inside your WHERE clause.

- Each WHEN clause contains 2 logical tests
	1. The first tests if a hometeam_id identifies Chelsea
	2. Then it tests if the home team scored higher than the away team
If both conditions are TRUE, the new column output returns the phrase "Chelsea home win!"

The oppposite set of conditions are included in a 2nd WHEN statement
	1. If the awayteam_id belongs to Chelsea
	2. AND scored higher, then the output returns "Chelsea away win!"
All other matches are categorized as a loss or tie 




# What ELSE is being excluded ?
- What's in your ==ELSE== clause ?
```mysql
SELECT date, hometeam_id, awayteam_id,
	CASE WHEN hometeam_id = 8455 AND home_goal > away_goal
		THEN 'Chelsea home win!'
	WHEN awayteam_id = 8455 AND home_goal < away_goal
		THEN 'Chelsea away win!'
	ELSE 'Loss or tie :(' END AS outcome
FROM match;
```

It is important to carefully consider which rows of your data are part of your ELSE clause, and if they're categorized correctly.

It is the same statement as before but, the WHERE filter has been removed.
	- Without this filter, your ELSE clause will categorize ALL matches played by anyone, who don't meet these first 2 conditions, as "Loss or tie :("



# Correctly categorize your data with CASE
```mysql
SELECT date, hometeam_id, awayteam_id,
	CASE WHEN hometeam_id = 8455 AND home_goal > away_goal
			THEN 'Chelsea home win!'
		WHEN awayteam_id = 8455 AND home_goal < away_goal
			THEN 'Chelsea away win!'
		ELSE 'Loss or tie :(' END AS outcome
FROM match
WHERE hometeam_id = 8455 OR awayteam_id = 8455;
```

The easiest way to correct for this to ensure you add specific filters in the WHERE clause that exclude all teams where chelsea did not play.

- Here, we specify this by using an OR statement in WHERE, which retrieves only results where the id 8455 is present in the hometeam_id or awayteam_id columns.



# What's NULL ?
```mysql
SELECT date,
CASE WHEN date > '2015-01-01' THEN 'More Recently'
	WHEN date < '2012-01-01' THEN 'Older'
	END AS date_category
FROM match;
SELECT date,
CASE WHEN date > '2015-01-01' THEN 'More Recently'
	WHEN date < '2012-01-01' THEN 'Older'
	ELSE NULL END AS date_category
FROM match;
```
| date       | date_category |
| ---------- | ------------- |
| 2011-11-18 | Older         |
| 2012-02-11 | NULL          |
| 2014-11-07 | NULL          |
| 2015-02-14 | More Recently              |

It's also important to consider what your ELSE clause is doing.

These 2 queries here are identical, except for the ELSE NULL statement specified in the 2nd.

They both return identical results -- a table with quite a few null results.
But what if you want to exclude them ?


# What are your NULL values doing ?
```mysql
SELECT date, season,
	CASE WHEN hometeam_id = 8455 AND home_goal > away_goal
			THEN 'Chelsea home win!'
		WHEN awayteam_id = 8455 AND home_goal < away_goal
			THEN 'Chelsea away win!'
		END AS outcome
FROM match
WHERE hometeam_id = 8455 OR awayteam_id = 8455;
```

| date       | seasson   | outcome           |
| ---------- | --------- | ----------------- |
| 2011-08-14 | 2011/2012 | NULL              |
| 2011-12-22 | 2011/2012 | NULL              |
| 2012-12-08 | 2012/2013 | Chelsea away win! |
| 2013-03-02 | 2012/2013 | Chelsea home win!                  |

Let's say we're only interested in viewing the results of games where Chelsea won, and we don't care if they lose or tie.
	- Just like in previous example, simply removing the ELSE clause will still retrieve those results -- and a lot of NULL values.



# Where to place your CASE ?
```mysql
SELECT date, season,
	CASE WHEN hometeam_id = 8455 AND home_goal > away_goal
			THEN 'Chelsea home win!'
		WHEN awayteam_id = 8455 AND home_goal < away_goal
			THEN 'Chelsea away win!' END AS outcome
FROM match
WHERE CASE WHEN hometeam_id = 8455 AND home_goal > away_goal
				THEN 'Chelsea home win!'
			WHEN awayteam_id = 8455 AND home_goal < away_goal
				THEN 'Chelsea away win!' END IS NOT NULL;
```
Treat your entire CASE statement as a column to filter by in your WHERE clause, just like any other column.

In order to filter a query by a CASE statement, you include the entire CASE statement, except its alias, in WHERE.
	- You then specify what you want to include, or exclude.

For this query, I want to keep all rows where this CASE statement IS NOT NULL.
My resulting table now only includes Chelsea's home and away wins and I don't need to filter by their team ID anymore.

----



# Case WHEN with aggregate functions

- What are CASE statements great at ?
	- Categorizing data
	- Filtering data
	- Aggregating data


## Counting CASES
- How many home and away goals did Liverpool score in each season ?
| season    | home_wins | away_wins |
| --------- | --------- | --------- |
| 2011/2012 |           |           |
| 2012/2013 |           |           |
| 2013/2014 |           |           |
| 2014/2015          |           |           |

- How do you get a count of liverpool's win in each season ?


# CASE WHEN with COUNT
```mysql
SELECT 
	season,
	COUNT(CASE WHEN hometeam_id = 8650
				AND home_goal > away_goal
				THEN id END) AS home_wins
FROM match
GROUP BY season;
```
- CASE statements are like any other column in your query.
	- You can include them inside an aggregate function.

- When this CASE statement is inside the COUNT function, it COUNTS every id returned by this CASE statement.


```mysql
SELECT 
	season,
	COUNT(CASE WHEN hometeam_id = 8650
				AND home_goal > away_goal
				THEN id END) AS home_wins
	COUNT(CASE WHEN awayteam_id = 8650 AND away_goal > home_goal
				THEN id END) AS away_wins
FROM match
GROUP BY season;
```





