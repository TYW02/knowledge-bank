
# Row Numbers
```postgresql
SELECT
	Year, Event, Country
	ROW_NUMBER() OVER() AS Row_N
FROM Summer_Medals
WHERE
	Medal = 'Gold';
```


# Enter ORDER BY
- ORDER BY in OVER orders the rows related to the current row
	- EXAMPLE: Ordering by year in descending order in ROW_NUMBER's OVER clause will assign 1 to the most recent year's rows
	


# Ordering by Year in descending order
```postgresql
SELECT
	Year, Event, Country
	ROW_NUMBER() OVER(ORDER BY Year DESC) AS Row_N
FROM Summer_Medals
WHERE
	Medal = 'Gold';
```

- Adding ORDER BY within OVER changed the basis on which the function assigned numbers to rows, assigning lower numbers to the more recent rows.


# Ordering by multiple columns
```postgresql
SELECT
	Year, Event, Country,
	ROW_NUMBER() OVER
		(ORDER BY Year DESC, Event ASC) AS Row_N
FROM Summer_Medals
WHERE
	Medal = 'Gold';
```
- You can order by multiple columns in the OVER clause, just like you normally can outside of it. That'll also change the numbers assigned to each row, since their positions have changed.



# Ordering in- and Outside OVER
```postgresql
SELECT
	Year, Event, Country
	ROW_NUMBER() OVER
		(ORDER BY Year DESC, Event ASC) AS Row_N
FROM Summer_Medals
WHERE
	Medal = 'Gold'
ORDER BY Country ASC, Row_N ASC;
```
- In this query, row numbers are assigned based on the year and the event, but the ordering outside OVER orders by country and row.
1. First, ROW_NUMBER will assign numbers based on the order within OVER. So the row numbers are given after sorting the table by year and event. 
2. After that, the ORDER outside of OVER takes over, and sorts the results of the table by Country and row number. 
	- Notice that the first row in the result isn't the row with number 1, because the two orders are based on different columns. From that, you can conclude that the ORDER inside OVER takes effect before the ORDER outside of it.


# Reigning Champion
- A reigning champion is a champion who's won both the previous and current years' competitions
- The previous and current year's champions need to be in the same row (in two different columns)
### Enter LAG
- LAG(Column, n) OVER(...) returns columns' value at the row n before the current row


# Current champtions
```postgresql
SELECT
	Year, Country AS Champion
FROM Summer_Medals
WHERE
	Year IN (1996, 2000, 2004, 2008, 2012)
	AND Gender = 'Men' AND Medal = 'Gold'
	AND Event = 'Discus Throw''
```



# Current and last champions
```postgresql
WITH Discus_Gold AS (
	SELECT 
		Year, Country AS Champion
	FROM Summer_Medals
	WHERE
		Year IN (1996, 2000, 2004, 2008, 2012)
		AND Gender = 'Men' AND Medal = 'Gold'
		AND Event = 'Discus Throw')
SELECT
	Year, Champion,
	LAST(Champion,1) OVER
		(ORDER BY Year ASC) AS Last_Champion
FROM Discus_Gold
ORDER BY Year ASC;
```



















































