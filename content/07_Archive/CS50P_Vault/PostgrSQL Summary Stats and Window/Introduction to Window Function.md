

# Window Functions
- Perform an operation across a set of rows that are somehow related to the current row 
- Similar to GROUP BY aggregate functions, but all rows remain in the output
### Uses
- Fetching values preceding or following rows (e.g. fetching the previous row's value)
	- Determining reigning champion status
	- Calculating growth over time
- Assigning ordinal ranks (1st, 2nd, etc.) to rows based on their values' position in a sorted list
- Running totals, moving averages



# Row numbers
```postgresql
SELECT
	Year, Event, Country
FROM Summer_Medals
WHERE
	Medal = 'Gold';
```



# Enter ROW_NUMBER
```postgresql
SELECT
	Year, Event, Country
	ROW_NUMBER() OVER() AS Row_N
FROM Summer_Medals
WHERE
	Medal = 'Gold';
```
- ROW_NUMBER assigns a number to each row. The OVER clause indicates that it's a window function. In this query, ROW_NUMBER simply adds a column with each row's number or index.


# Anatomy of a Window Function

```postgresql
SELECT
	Year, Event, Country,
	ROW_NUMBER() OVER() AS Row_N
FROM Summer_Medals
WHERE
	Medal = 'Gold';
```
- Function_Name() OVER()
	- ORDER BY
	- PARTITION BY
	- ROWS/RANGE PRECEDING/FOLLOWING/UNBOUNDED












































