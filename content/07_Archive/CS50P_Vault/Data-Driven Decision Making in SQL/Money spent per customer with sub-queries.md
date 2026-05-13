

# Subsequent SELECT statements - actresses
- Query 1:
```postgresql
SELECT *
FROM actors
WHERE gender = 'female';
```

- Group result table of query 1 by nationality
- Report year of birth for the oldest and youngest actress in each country.
```postgresql
SELECT af.nationality,
	MIN(af.year_of_birth),
	MAX(af.year_of_birth)
FROM 
	(SELECT *
	FROM actors
	WHERE gender = 'female') AS af
GROUP BY af.nationality;
```



# Result subsequent SELECT statement - actresses
```postgresql
SELECT af.nationality,
	MIN(af.year_of_birth),
	MAX(af.year_of_birth)
FROM 
	(SELECT *
	FROM actors
	WHERE gender = 'female') AS af
GROUP BY af.nationality;
```



# How much money did each customer spend ?
- First step: Add renting_price from movies to table renting.
```postgresql
SELECT r.customer_id
	m.renting_price
FROM renting AS r
LEFT JOIN movies AS m
ON r.movie_id=m.movie_id;
```

- Second step:
	- Group result table from first step by customer_id
	- take the sum of renting_price
```postgresql
SELECT rm.customer_id,
	SUM(rm.renting_price)
FROM
	(SELECT r.customer_id,
		m.renting_price
	FROM renting AS r
	LEFT JOIN movies AS m
	ON r.movie_id=m.movie_id) AS rm
GROUP BY rm.customer_id;
```





























