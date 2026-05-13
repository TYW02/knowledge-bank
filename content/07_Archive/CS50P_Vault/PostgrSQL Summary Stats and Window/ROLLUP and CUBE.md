
# The old way
![[Pasted image 20230119093758.png]]


# Enter ROLLUP
```postgresql
SELECT
	Country, Medal, COUNT(*) AS Awards
FROM Summer_Medals
WHERE
	Year = 2008 AND Country IN ('CHN', 'RUS')
GROUP BY Country, ROLLUP(Medal)
ORDER BY Country ASC, Medal ASC;
```
- ROLLUP is a GROUP BY subclause that includes extra rows for group-level aggregations
- GROUP BY Country, ROLL(Medal) will count all Country - and Medal -level totals, then count only Country -level totals and fill in Medal with nulls for these rows


# ROLLUP - Query
```postgresql
SELECT
	Country, Medal, COUNT(*) AS Awards
FROM summer_medals
WHERE
	Year = 2008 AND Country IN ('CHN', 'RUS')
GROUP BY ROLLUP(Country, Medal)
ORDER BY Country ASC, Medal ASC;
```
- ROLLUP is hierarchical, de-aggregating from the leftmost provided column to the right-most
	- ROLLUP(Country, Medal) includes Country-level totals
	- ROLLUP(Medal, Country) includes Medal-level totals
	- Both include grand totals



# ROLLUP - Result
| Country | Medal  | Awards |
| ------- | ------ | ------ |
| CHN     | Bronze | 57     |
| CHN     | Gold   | 74     |
| CHN     | Sliver | 53     |
| CHN     | null   | 184       |
- Group-level totals contain nulls; the row with all nulls is the grand total
- Notice that it didn't include Medal-level totals, since it's ROLLUP(Country, Medal) and not ROLLUP(Medal, Country)


# Enter CUBE
```postgresql
SELECT
	Country, Medal, COUNT(*) AS Awards
FROM summer_medals
WHERE
	Year = 2008 AND Country IN ('CHN', 'RUS')
GROUP BY CUBE(Country, Medal)
ORDER BY Country ASC, Medal ASC;
```
- CUBE is non-hierarchical ROLLUP
- It generates all possible group-level aggregations
	- CUBE(Country, Medal) counts Country-level, Medal-level, and grand totals


# ROLLUP vs CUBE
- Source
| Year | Quarter | Sales |
| ---- | ------- | ----- |
| 2008 | Q1      | 12    |
| 2008 | Q2      | 15    |
| 2009 | Q1      | 21    |
| 2009 | Q2      | 27      |
- Use ROLLUP when you have hierarchical data (e.g. date parts) and don't want all possible group-level aggregations
- Use CUBE when you want all possible group-level aggregations


- ROLLUP(Year, Quarter)
| Year | Quarter | Sales |
| ---- | ------- | ----- |
| 2008 | null    | 27    |
| 2009 | null    | 48    |
| null | null    | 75    |


- CUBE(Year, Quarter)
Above rows + the following
| Year | Quarter | Sales |
| ---- | ------- | ----- |
| null | Q1      | 33    |
| null | Q2     | 42      |














































