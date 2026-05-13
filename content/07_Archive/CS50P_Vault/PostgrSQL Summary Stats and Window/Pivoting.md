
# Transforming Tables
- Before
| Country | Year | Awards |
| ------- | ---- | ------ |
| CHN     | 2008 | 74     |
| CHN     | 2012 | 56     |
| RUS     | 2008 | 43     |
| RUS     | 2012 | 47     |
| USA     | 2008 | 125    |
| USA     | 2012 | 147       |

- Gold medals awarded to China, Russia, and the USA

- After
| Country | 2008 | 2012 |
| ------- | ---- | ---- |
| CHN     | 74   | 56   |
| RUS     | 43   | 47   |
| USA     | 125  | 147     |
- Pivoted by Year
- Easier to scan, especially if pivoted by a chronologically ordered column



# Enter CROSSTAB
```postgresql
CREATE EXTENSION IF NOT EXISTS tablefunc;

SELECT * FROM CROSSTAB($$
	source_sql TEXT
	$$) AS ct (column_1 DATA_TYPE_1,
				column_2 DATA_TYPE_2,
				...,
				column_n DATA_TYPE_N);
```



# Queries
- Before
```postgresql
SELECT
	Country, Year, COUNT(*) AS Awards
FROM Summer_Medals
WHERE
	Country IN ('CHN', 'RUS', 'USA')
	AND Year IN (2008, 2012)
	AND Medal = 'Gold'
GROUP BY Country, Year
ORDER BY Country ASC, Year ASC;
```

- After
```postgresql
CREATE EXTENSION IF NOT EXISTS tablefunc;

SELECT * FROM CROSSTAB($$
	SELECT
		Country, Year, COUNT(*) :: INTEGER AS Awards
	FROM Summer_Medals
	WHERE
		Country IN ('CHN', 'RUS', 'USA')
		AND Year IN (2018, 2O12)
		AND Medal = 'Gold'
	GROUP BY Country, Year
	ORDER BY Country ASC, Year ASC;
$$) AS ct (Country VARCHAR, "2008" INTEGER, "2012" INTEGER)

ORDER BY Country ASC;
```


# Source Query
```postgresql
WITH Country_Awards AS (
	SELECT
		Country, Year, COUNT(*) AS Awards
	FROM Summer_Medals
	WHERE
		Country IN ('CHN', 'RUS', 'USA')
		AND Year IN (2004, 2008, 2012)
		AND Medal = 'Gold' AND Sport = 'Gymnastics'
	GROUP BY Country, Year
	ORDER BY Country ASC, Year ASC)

SELECT 
	Country, Year,
	RANK() OVER
		(PARTITIOIN BY Year ORDER BY Awards DESC) :: INTEGER
		AS rank
	FROM Country_Awards
ORDER BY Country ASC, Year ASC;
```


# Pivot query
```postgresql
CREATE EXTENSION IF NOT EXISTS tablefunc;

SELECT * FROM CROSSTAB($$
	...
$$) AS ct (Country VARCHAR,
			  "2004" INTEGER,
			  "2008" INTEGER,
			  "2012" INTEGER)
ORDER BY Country ASC;
```
































