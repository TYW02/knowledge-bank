

# Overview of OLAP operators in SQL
Extensions in SQL to facilitate OLAP operations
- GROUP BY CUBE
- GROUP BY ROLLUP
- GROUP BY GROUPING SETS


# GROUP BY GROUPING SETS
Example of a query with GROUPING SETS operator:
```postgresql
SELECT country,
	genre,
	COUNT(*)
FROM rentings_extended
GROUP BY GROUPING SETS ((country, genre), (country), (genre), ());
```

- Column names surrounded by parentheses represent one level of aggregation.
- GROUP BY GROUPING SETS returns a UNION over several GROUP BY queries.


# GROUPING SETS and GROUP BY queries
```postgresql
SELECT country,
	genre,
	COUNT(*)
FROM renting_extended
GROUP BY GROUPING SETS(country, genre);
```
- Count movie rentals for each unique combination of country and genre.
- Expression in GROUPING SETS: (countrym genre)


```postgresql
SELECT country,
	genre,
	COUNT(*)
FROM renting_extended
GROUP BY country, genre;
```


```postgresql
SELECT COUNT(*)
FROM renting_extended
GROUP BY GROUPING SETS ();
```
- Total aggregation - count all movie rentals.
- Expresssion in GROUPING SETS: ()


# Notation for GROUP BY GROUPING SETS
- GROUP BY GROUPING SETS (...)
```postgresql
SELECT country, genre, COUNT(*)
FROM renting_extended
GROUP BY GROUPING SETS ((country, genre), (country), (genre), ());
```
- UNION over 4 previous queries.
- Combine all information of a pivot table in one query.
- This query is equivalent to GROUP BY CUBE (country, genre).


# Result with GROUPING SETS operator
```postgresql
SELECT country, genre, COUNT(*)
FROM renting_extended
GROUP BY GROUPING SETS ((country, genre), (country), (genre),());
```



# Calculate number of rentals and average rating
```postgresql
SELECT country, genre, COUNT(*), AVG(rating) AS avg_rating
FROM renting_extended
GROUP BY GROUPING SETS ((country, genre), (genre));
```































