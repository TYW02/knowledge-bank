

# Source Table
```postgresql
SELECT
	Year, COUNT(*) AS Medals
FROM Summer_Medals
WHERE
	Country = 'BRA'
	AND Medal = 'Gold'
	AND Year >= 1992
GROUP BY Year
ORDER BY Year ASC;
```



# Aggregate Functions
- MAX Query
```postgresql
WITH Brazil_Medals AS (...)

SELECT MAX(Medals) AS Max_Medals
FROM Brazil_Medals;
```

- SUM Query
```postgresql
WITH Brazil_Medals AS (...)

SELECT SUM(Medals) AS Total_Medals
FROM Brazil_Medals;
```


# MAX Window Function
```postgresql
WITH Brazil_Medals AS (...)

SELECT
	Year, Medals,
	MAX(Medals)
		OVER(ORDER BY Year ASC) AS Max_Medals
FROM Brazil_Medals;
```


# SUM Window Function
```postgresql
WITH Brazil_Medals AS (...)

SELECT 
	Year, Medals,
	SUM(Medals) OVER (ORDER BY Year ASC) AS Medals_RT
FROM Brazil_Medals;
```

# Partitioning with aggregate window functions
```postgresql
WITH Medals AS (...)
SELECT Year, Country, Medals,
	SUM(Medals) OVER (...)
FROM Medals;
```

```postgresql
WITH Medals AS (...)
SELECT Year, Country, Medals,
	SUM(Medals) OVER (PARTITION BY Country ...)
FROM Medals;
```























