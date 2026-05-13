


# Introduction to OLAP
- OLAP: on-line analytical processing
- Aggregate data for a better overview
	- Count number of rentings for each customer
	- Average rating of movies for each genre and each country
- Produce pivot tables to present aggregation results



# GROUP BY CUBE
```postgresql
SELECT country,
	genre,
	COUNT(*)
FROM renting_extended
GROUP BY CUBE (country, genre);
```


# Number of ratings
```postgresql
SELECT country,
	genre,
	COUNT(rating)
FROM renting_extended
GROUP BY CUBE(country, genre);
```
































