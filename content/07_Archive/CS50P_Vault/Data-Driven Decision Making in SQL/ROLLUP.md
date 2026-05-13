
# Query with ROLLUP
```postgresql
SELECT country,
	genre,
	COUNT(*)
FROM renting_extended
GROUP BY ROLLUP (country, genre);
```
- Levels of aggregation
	- Aggregation of each combination of country and genre
	- Aggregation of country alone
	- Total Aggregation



# Summary ROLLUP
- Returns aggrefates for a hierarchy of values, e.g. ROLLUP(country, genre)
	- Movie rentals for each country and each genre
	- Movie rentals for each country
	- Total number of movie rentals
- In each step, one level of detail is dropped
- Order of column names is important for ROLLUP


# Number of rentals and ratings
```postgresql
SELECT country,
	genre,
	COUNT(*) AS n_rentals,
	COUNT(rating) AS n_ratings
FROM renting_extended
GROUP BY ROLLUP (genre, country);
```

































