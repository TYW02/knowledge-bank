
# Example - UNION
```postgresqL
SELECT title,
	genre,
	renting_price
FROM movies
WHERE renting_price > 2.8
UNION
SELECT title,
	genre,
	renting_price
FROM movies
WHERE genre = 'Action & Adventure';
```


# Example - INTERSECT
```postgresql
SELECT title,
	genre,
	renting_price
FROM movies
WHERE renting_price > 2.8
INTERSECT
SELECT title,
	genre,
	renting_price
FROM movies
WHERE genre = 'Action & Adventure';
```


























































