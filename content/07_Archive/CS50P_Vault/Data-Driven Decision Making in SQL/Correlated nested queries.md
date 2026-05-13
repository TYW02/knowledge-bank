
# Correlated queries
- Condition in the WHERE clause of the inner query
- Refereneces some column of a table in the outer query


# Example correlated query
- Number of movie rentals more than 5
```postgresql
SELECT *
FROM movies AS m
WHERE 5 <
	(SELECT COUNT(*)
	FROM renting AS r
	WHERE r.movie_id=m.movie_id);
```


# Evaluate inner query
```postgresql
SELECT COUNT(*)
FROM renting AS r
WHERE r.movie_id = 1;
```



# Evaluate outer query
Number of movie rentals larger than 5
```postgresql
SELECT *
FROM movie as m
WHERE 5 <
	(SELECT COUNT(*)
	FROM renting as r
	WHERE r.movie_id = m.movie_id);
```


Select movies with less than 5 movie rentals.
```postgresql
SELECT *
FROM movie as m
WHERE 5 >
	(SELECT COUNT(*)
	FROM renting as r
	WHERE r.movie_id = m.movie_id);
```











































