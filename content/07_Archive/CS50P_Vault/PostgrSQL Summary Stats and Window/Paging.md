

# What is paging ?
- Paging: Splitting data into (approximately) equal chunks
- Uses
	- Many APIs return data in "pages" to reduce data being sent
	- Separating data into quartiles or thirds (top middle 33%, and bottom thirds) to judge performance
Enter NTILE
- NTILE(n) splits the data into n approximately equal pages


# Paging - Source Table
```postgresql
SELECT
	DISTINCT Discipline
FROM Summer_Medals;
```
- Splits the data into 15 approx. equally sized pages
- 67/15 ~= 4, so each each page will contain four or five rows



# Paging
```postgresql
WITH Disciplines AS (
	SELECT
		DISTINCT Discipline
	FROM Summer_Medals)
SELECT
	Discipline, NTILE(15) OVER() AS Page
FROM Disciplines
ORDER BY Page ASC;
```


# Top, middle, and bottom thirds
```postgresql
WITH Country_Medals AS (
	SELECT 
		Country, COUNT(*) AS Medals
	FROM Summer_Medals
	GROUP BY Country),
SELECT
	Country, Medals,
	NTILE(3) OVER(ORDER BY Medals DESC) AS Third
FROM Country_Medals;
```


# Thirds Averages
```postgresql
WITH Country_Medals AS (...)

	Thirds AS (
	SELECT 
		Country, Medals,
		NTILE(3) OVER (ORDER BY Medals DESC) AS Third
	FROM Country_Medals)
SELECT
	Third,
	ROUND(AVG(Medals), 2) AS Avg_Medals
FROM Thirds
GROUP BY Third
ORDER BY Third ASC;
```



















































