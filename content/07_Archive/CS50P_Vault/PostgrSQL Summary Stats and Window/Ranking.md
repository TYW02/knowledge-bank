

# The Ranking Functions
- ROW_NUMBER() always assigns unique numbers, even if 2 rows' values are the same
- RANK() assigns the same number to rows with identical values, skipping over the next numbers in such cases
- DENSE_RANK() also assigns the same number to rows with identical values, but doesn't skip over the next numbers.



# Source Table
```postgresql
SELECT
	Country, COUNT(DISTINCT Year) AS Games
FROM Summer_Medals
WHERE
	Country IN (
		'GBR', 'DEN', 'FRA',
		'ITA', 'AUT', 'BEL',
		'NOR', 'POL', 'ESP'
	)
GROUP BY Country
ORDER BY Games DESC;
```


# Different Ranking Functions - ROW_NUMBER
```postgresql
WITH Country_Games AS (...)

SELECT 
	Country, Games,
	ROW_NUMBER()
		OVER(ORDER BY Games DESC) AS Row_N
FROM Country_Games
ORDER BY Games DESC, Country ASC;
```



# Different Ranking Functions - RANK
```postgresql
WITH Country_Games AS (...)

SELECT 
	Country, Games,
	ROW_NUMBER()
		OVER(ORDER BY Games DESC) AS Row_N,
	RANK()
		OVER(ORDER BY Games DESC) AS Rank_N
FROM Country_Games
ORDER BY Games DESC, Country ASC;
```



# Different Ranking Functions - DENSE_RANK
```postgresql
WITH Country_Games AS (...)

SELECT
	Country, Games,
	ROW_NUMBER()
		OVER(ORDER BY Games DESC) AS Row_N,
	RANK()
		OVER(ORDER BY Games DESC) AS Rank_N,
	DENSE_RANK()
		OVER(ORDER BY Games DESC) AS Dense_Rank_N
FROM Country_Games
ORDER BY Games DESC, Country ASC;
```
- ROW_NUMBER and RANK will have the same last rank, the count of rows


# Ranking without partitioning - Source Table
```postgresql
SELECT 
	Country, Athlete, COUNT(*) AS Medals
FROM Summer_Medals
WHERE 
	Country IN ('CHN', 'RUS')
	AND Year = 2012
GROUP BY Country, Athlete
HAVING COUNT(*) > 1
ORDER BY Country ASC, Medals DESC;
```


# Ranking without Partitioning
```postgresql
WITH Country_Medals AS (...)

SELECT
	Country, Athlete, Medals,
	DENSE_RANK()
		OVER(ORDER BY Medals DESC) AS Rank_N
FROM Country_Medals
ORDER BY Country ASC, Medals DESC;
```

# Ranking with Partitioning
```postgresql
WITH Country_Medals AS (...)

SELECT
	Country, Athlete,
	DENSE_RANK()
		OVER(PARTITION BY Country
			ORDER BY Medals DESC) AS Rank_N
FROM Country_Medals
ORDER BY Country ASC, Medals DESC;
```
















































































