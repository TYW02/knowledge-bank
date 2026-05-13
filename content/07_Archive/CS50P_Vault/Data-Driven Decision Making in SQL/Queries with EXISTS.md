

# EXISTS
- Special case of a correlated nested query
- Used to check if result of a correlated nested query is empty
- It returns: TRUE or FALSE
- TRUE = not empty -> row of the outer query is selected
- FALSE = empty
- Columns specified in SELECT component not considered -use SELECT *



# Movies with at least one rating
```postgresql
SELECT *
FROM movies AS m
WHERE EXISTS
	(SELECT *
	FROM renting AS r
	WHERE rating IS NOT NULL
	AND r.movie_id = m.movie_id);
```


```postgresql
SELECT *
FROM renting AS r
WHERE rating IS NOT NULL
AND r.movie_id = 11;
```


```postgresql
SELECT *
FROM renting AS r
WHERE rating IS NOT NULL
AND r.movie_id = 1;
```


# EXISTS query with result
```postgresql
SELECT *
FROM movies AS m
WHERE EXISTS
	(SELECT *
	FROM renting AS r
	WHERE rating IS NOT NULL
	AND r.movie_id = m.movie_id);
```


# NOT EXISTS
- TRUE = table is empty -> row of the outer query is selected.
```postgresql
SELECT *
FROM movies AS m
WHERE NOT EXISTS
	(SELECT *
	FROM renting AS r
	WHERE rating IS NOT NULL
	AND r.movie_id = m.movie_id);
```
































