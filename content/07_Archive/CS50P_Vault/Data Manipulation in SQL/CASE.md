
## Selecting from the European Soccer Datbase
```mysql
SELECT
	l.name AS league,
	COUNT(m.country_id) AS total_matches
FROM league AS l
LEFT JOIN match AS m
ON l.country_id = m.country_id
GROUP BY l.name;
```

| league | total_matches |
|---|---|
| Belgium Jupiler League | 732 |
|England Premier League | 1520|
|France Ligue 1 | 1520 |
|Germany 1. Bundesliga| 1224|


```mysql
	SELECT
		date,
		id,
		home_goal,
		away_goal
	FROM match
	WHERE season = '2013/2014';
```

| date | id| home_goal| away_goal|
|----|----|----|----|
| 2014-03-09 00:00:00| 1237 | 2 | 0 |
| 2014-03-29 00:00:00 | 1238 | 0 | 1|
| 2014-04-05 00:00:00 | 1239 | 1 | 0|
|2014-0405 00:00:00| 1240 | 0 | 0|


# Case Statement
#CaseStatement

- Contains a ==WHEN==, ==THEN==, and ==ELSE== statement, finished with ==END==
```mysql
CASE WHEN x = 1 THEN 'a'
	WHEN x = 2 THEN 'b'
	ELSE 'c' END AS new_column
```

- Case statements are SQL's version of an "IF this THEN that" statement.

#### Case Statements have 3 parts
1. WHEN
	- Tests a given condition (x = 1)
	- If TRUE move to THEN
2. THEN
3. ELSE
	- The CASE statement is ended with an ELSE clause that returns a specified value if all of your when statements are **not** true.
4. END
	- Be sure to include END and give your statement an alias


## CASE WHEN
```mysql
SELECT
	id,
	home_goal,
	away_goal,
	CASE WHEN home_goal > away_goal THEN 'Home Team Win'
		WHEN home_goal < away_goal THEN 'Away Team Win'
		ELSE 'Tie' END AS outcome
FROM match
WHERE season = '2013/2014'
```

| id   | home_goal | away_goal | outcome       |
| ---- | --------- | --------- | ------------- |
| 1237 | 2         | 0         | Home Team Win |
| 1238 | 0         | 1         | Away Team Win |
| 1239 | 1         | 0         | Home Team Win |
| 1240 | 0         | 0         | Tie              |

- In this example, we use a CASE statement to create a new variable that identifies matches as home team wins, away team wins, or ties.

- A new column is created with the appropriate text for each match given the outcome.

---
