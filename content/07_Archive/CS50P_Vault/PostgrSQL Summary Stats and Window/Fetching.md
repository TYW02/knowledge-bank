
# The Four Functions
## Relative
- LAG(column, n) returns column's value at the row n rows before the current row
- LEAD(column, n) returns column's value at the row n rows after the current row
## Absolute
- FIRST_VALUE(column) returns the first value in the table or partition
- LAST_VALUE(column) returns the last value in the table or partition


# LEAD
```postgresql
WITH Hosts AS (
	SELECT DISTINCT Year, City
	FROM Summer_Medals)
SELECT
	Year, City,
	LEAD(City, 1) OVER (ORDER BY Year ASC)
		AS Next_City,
	LEAD(City, 2) OVER (ORDER BY Year ASC)
		AS After_Next_City
FROM Hosts
ORDER BY Year ASC;
```


# FIRST_VALUE and LAST_VALUE
```postgresql
SELECT
	Year, City,
	FIRST_VALUE(City) OVER
		(ORDER BY Year ASC) AS First_city,
	LAST_VALUE(City) OVER (
		ORDER BY Year ASC
		RANGE BETWEEN
			UNBOUNDED PRECEDING AND
			UNBOUNDED FOLLOWING
	) AS last_city
FROM Hosts
ORDER BY Year ASC;
```
- By default, a window starts at the beginning of the table or partition and ends at the current row
- RANGE BETWEEN... clause extends the window to the end of the table or partition


# Partitioning with LEAD
- LEAD(Champion, 1) without PARTITION BY
![[Pasted image 20230116135212.png]]

- LEAD(Champion, 1) with PARTITION BY Event
![[Pasted image 20230116135244.png]]


# Partitioning with FIRST_VALUE
- FIRST_VALUE(Champion) without PARTITION BY Event
![[Pasted image 20230116135321.png]]

- FIRST_VALUE(Champion) with PARTITION BY Event
![[Pasted image 20230116135344.png]]
























