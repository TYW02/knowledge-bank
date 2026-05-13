
# Enter PARTITION BY
- PARTITION BY splits the table into partitions based on a column's unique values
	- The results aren't rolled into one column
- Operated on separately by the window function
	- ROW_NUMBER will reset for each partition
	- LAG will only fetch a row's previous value if its previous row is in the same person


# Partitioning by one column
```postgresql
WITH Discus_Gold AS (...)

SELECT 
	Year, Event, Champion,
	LAG(Champion) OVER
	(PARTITION BY Event
	ORDER BY Event ASC, Year ASC) AS Last_Champion
FROM Discus_Gold
ORDER BY Event ASC, Year ASC;
```


# Partitioning by Multiple Columns
```postgresql
WITH Country_Gold AS (
	SELECT
		DISTINCT Year, Country, Event
	FROM Summer_Medals
	WHERE
		Year IN (2008, 2012)
		AND Country IN ('CHN', 'JPN')
		AND Gender = 'Women' AND Medal = 'Gold')
SELECT 
	Year, Country, Event,
	ROW_NUMBER() OVER(PARTITION BY Year, Country)
FROM Country_Gold;
```














































