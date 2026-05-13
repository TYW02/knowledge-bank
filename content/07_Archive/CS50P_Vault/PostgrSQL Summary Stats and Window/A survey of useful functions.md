

# Nulls ahoy
```postgresql
SELECT
	Country, Medal, COUNT(*) AS Awards
FROM summer_medals
WHERE
	Year = 2008 AND Country IN ('CHN', 'RUS')
GROUP BY ROLLUP(Country, Medal)
ORDER BY Country ASC, Medal ASC;
```


# Enter COALESCE
- COALESCE() take a list of values and returns the first non-null value, going from left to right
- COALESCE(null, null, 1, null, 2) ? 1
- Useful when using SQL operations that return null
	- ROLLUP and CUBE
	- Pivoting
	- LAG and LEAD


# Annihilating nulls
```postgresql
SELECT
	COALESCE(Country, 'Both countries') AS Country,
	COALESCE(Medal, 'All medals') AS Medal,
	COUNT(*) AS Awards
FROM summer_medals
WHERE
	Year = 2008 AND Country IN ('CHN', 'RUS')
GROUP BY ROLLUP(Country, Medal)
ORDER BY Country ASC, Medal ASC;
```


# Compressing Data
- Before
| Country | Rank |
| ------- | ---- |
| CHN     | 1    |
| RUS     | 2    |
| USA     | 3     |
- RANK is redundant because the ranking is implied

- After
CHN, RUS, USA
- Succinct and provides all information needed because the ranking is implied


# Enter STRING_AGG
- STRING_AGG(column, separator) takes all the values of a column and concatenates them, with separator in between each value
STRING_AGG(Letter, ',') transforms this...
| Letter |
| ------ |
| A      |
| B      |
| C       |
... into this
A, B, C


# Query and result
- Before
```postgresql
WITH Country_Medals AS (
	SELECT
		Country, COUNT(*) AS Medals
	FROM Summer_Medals
	WHERE Year = 2012
		AND Country IN ('CHN', 'RUS', 'USA')
		AND Medal = 'Gold'
		AND Sport = 'Gymnastics'
	GROUP BY Country)

	SELECT
		Country,
		RANK() OVER (ORDER BY Medals DESC) AS Rank
	FROM Country_Medals
	ORDER BY Rank ASC;
```

- After
```postgresql
WITH Country_Medals AS (...),
	Country_Ranks AS (...)
	SELECT STRING_AGG(Country, ',')
	FROM Country_Medals;
```































