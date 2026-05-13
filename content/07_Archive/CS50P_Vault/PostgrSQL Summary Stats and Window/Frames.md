

# Motivation
LAST_VALUE
```postgresql
LAST_VALUE(City) OVER (
ORDER BY Year ASC
RANGE BETWEEN 
	UNBOUNDED PRECEDING AND
	UNBOUNDED FOLLOWING
) AS Last_city
```
- Frame: RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING
- Without the frame, LAST_VALUE would return the row's value in the City column
- By default, a frame starts at the beginning of a table or partition and ends at the current row



# ROWS BETWEEN
- ROWS BETWEEN [START] AND [FINISH]
- n PRECEDING: n rows before the current row
- CURRENT ROW: the current row
- n FOLLOWING: n rows after the current row
## Examples
- ROWS BETWEEN 3 PRECEDING AND CURRENT ROW
- ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING
- ROWS BETWEEN 5 PRECEDING AND 1 PRECEDING


# Source table
```postgresql
SELECT
	Year, COUNT(*) AS Medals
FROM Summer_Medals
WHERE
	Country = 'RUS'
	AND Medal = 'Gold'
GROUP BY Year
ORDER BY Year ASC;
```


# MAX without a frame
```postgresql
WITH Russia_Medals AS (...)

SELECT 
	Year, Medals,
	MAX(Medals)
		OVER(ORDER BY Year ASC) AS Max_Medals
FROM Russia_Medals
ORDER BY Year ASC;
```



# MAX with a frame
```postgresql
WITH Russia_Medals AS (...)

SELECT
	Year, Medals,
	MAX(Medals)
		OVER(ORDER BY Year ASC) AS Max_Medals,
	MAX(Medals)
		OVER(ORDER BY Year ASC
		ROWS BETWEEN 
		1 PRECEDING AND CURRENT ROW)
	AS Max_Medals_Last
FROM Russia_Medals
ORDER BY Year ASC;
```



# Current and following rows
```postgresql
WITH Russia_Medals AS (...)

SELECT 
	Year, Medals,
	MAX(Medals)
	OVER(ORDER BY Year ASC
		ROWS BETWEEN 
		CURRENT ROW AND 1 FOLLOWING)
	AS Max_Medals_Next
FROM Russia_Medals
ORDER BY Year ASC;
```





























