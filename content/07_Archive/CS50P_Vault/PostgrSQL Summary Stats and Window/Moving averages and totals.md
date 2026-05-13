

# Overview
- Moving average (MA): Average of last n periods
	- Example: 10-day MA of units sold in sales is the average of the last 10 days' sold units 
	- Used to indicate momentum/trends
	- Also useful in eliminating seasonality
- Moving total: Sum of last n periods
	- Example: Sum of the last 3 Olympic games' medals
	- Used to indicate performance; if the sum is going down, overall performance is going down


# Moving Average
```postgresql
WITH US_Medals AS (...)

SELECT
Year, Medals,
AVG(Medals) OVER
(ORDER BY Year ASC
ROWS BETWEEN
2 PRECEDING AND CURRENT ROWS) AS Medals_MA
FROM US_Medals
ORDER BY Year ASC;
```


# Moving Total
```postgresql
WITH US_Medals AS (...)

SELECT
	Year, Medals,
	SUM(Medals) OVER
		(ORDER BY Year ASC
		ROWS BETWEEN
		2 PRECEDING AND CURRENT ROW) AS Medals_MT
FROM US_Medals
ORDER BY Year ASC;
```




# ROWS vs RANGE
- RANGE BETWEEN [START] AND [FINISH]
	- Functions much the same as ROWS BETWEEN
	- RANGE treats duplicates in OVER's ORDER BY subclause as a single entity

- ROWS BETWEEN is almost always used over RANGE BETWEEN

































