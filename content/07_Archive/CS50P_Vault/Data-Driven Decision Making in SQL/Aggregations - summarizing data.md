

# Overview aggregations
```postgresql
SELECT AVG(renting_price)
FROM movies;
```

- Some aggregate functions in SQL
	- AVG()
	- SUM()
	- COUNT()
	- MIN()
	- MAX()



# Aggregation with NULL values
```postgresql
SELECT COUNT(*)
FROM actors;
```

```postgresql
SELECT COUNT(name)
FROM actors;
```

```postgresql
SELECT COUNT(year_of_birth)
FROM actors;
```



# DISTINCT
```postgresql
SELECT DISTINCT country
FROM customers;
```

```postgresql
SELECT COUNT(DISTINCT country)
FROM customers;
```



# DISTINCT with 'NULL' values
```postgresql
SELECT DISTINCT rating
FROM renting
ORDER BY rating;
```



# Give an alias to column names
```postgresql
SELECT AVG(renting_price) AS average_price,
	COUNT(DISTINCT genre) AS number_genres
FROM movies;
```

- Helps to understand the result when column names are self-explaining



































