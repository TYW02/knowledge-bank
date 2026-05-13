

# Nested query
- SELECT block in WHERE or HAVING clauses
- Inner query returns single or multiple values
- Use result from the inner query to select specific rows in another query


# The inner query

- Step 1: The inner query
```postgresql
SELECT DISTINCT customer_id
FROM renting
WHERE rating <= 3
```



# Result in the WHERE clause
```postgresql
SELECT name
FROM customers
WHERE customer_id IN (28, 41, 86, 120);
```



# The outer query

- Step 2: The outer query
```postgresql
SELECT name
FROM customers
WHERE customer_id IN
	(SELECT DISTINCT customer_id
	FROM renting
	WHERE rating <= 3);
```



# Nested query in the HAVING clause

- Step 1: The inner query
```postgresql
SELECT MIN(date_account_start)
FROM customers
WHERE country = 'Austria';
```


- Step 2: The outer query
```postgresql
SELECT country, MIN(date_account_start)
FROM customers
GROUP BY country
HAVING MIN(date_account_start) < 
	(SELECT MIN(date_account_start)
	FROM customers
	WHERE country = 'Austria');
```


# Who are the actors in the movie Ray?
```postgresql
SELECT name
FROM actors
WHERE actor_id IN
	(SELECT actor_id
	FROM actsin
	WHERE movie_id = 
		(SELECT movie_id
		FROM movies
		WHERE title='Ray'));
```






































