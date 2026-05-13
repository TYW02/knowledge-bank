

# GROUP BY Applications
- Perferences of customers by country or gender
- The popularity of movies by genre or year of release.
- The average prce of movies by genre


# GROUP BY
```postgresql
SELECT genre
FROM movies_selected
GROUP BY genre;
```



# Average renting price
```postgresql
SELECT genre,
	AVG(renting_price) AS avg_price
FROM movies_selected
GROUP BY genre;
```




# Average rental price and number of movies
```postgresql
SELECT genre,
	AVG(renting_prices) AS avg_prices,
	COUNT(*) AS number_movies
FROM movies_selected
GROUP BY genre
```



# HAVING
```postgresql
SELECT genre,
	AVG(renting_price) avg_prices,
	COUNT(*) number_movies
FROM movies
GROUP BY genre
HAVING COUNT(*) > 2;
```




































