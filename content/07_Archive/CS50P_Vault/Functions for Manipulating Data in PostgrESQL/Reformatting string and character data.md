

# The string concatenation operator
```postgresql
SELECT
	first_name,
	last_name,
	first_name || ' ' || last_name AS full_name
FROM customer
```

```postgresql
+------------------+---------------+------------------+
| first_name       | last_name     | full_name        |
|------------------|---------------|------------------|
| MARY             | SMITH         | MARY SMITH       |
| LINDA            | WILLIAMS      | LINDA WILLIAMS   |
+------------------+---------------+------------------+
```


# String concatenation with functions
```postgresql
SELECT
	CONCAT(first_name, ' ', last_name) AS full_name
FROM customer;
```

```postgresql
+------------------+---------------+------------------+
| first_name       | last_name     | full_name        |
|------------------|---------------|------------------|
| MARY             | SMITH         | MARY SMITH       |
| LINDA            | WILLIAMS      | LINDA WILLIAMS   |
+------------------+---------------+------------------+
```




# String concatenation with a non-string input 
```postgresql
SELECT
	customer_id || ': '
	|| first_name || ' '
	|| last_name AS full_name
FROM customer;
```

```postgresql
+-------------------+
| full_name         |
|-------------------|
| 1: MARY SMITH     |
| 2: LINDA WILLIAMS |
+-------------------+
```



# Changing the case of string
```postgresql
SELECT
	UPPER(email)
FROM customer;
```


```postgresql
SELECT
	LOWER(title)
FROM film;
```



# Replacing characters in a string
```postgresql
SELECT 
	REPLACE(description, 'A Astounding',
				'An Astounding') AS description
FROM film;
```




# Manipulating string data with REVERSE
```postgresql
SELECT 
	title,
	REVERSE(title)
FROM 
	film AS f;
```







































