

# LEFT JOIN
- LEFT JOIN is an outer join
- Keep all rows of the left table, match with rows in the right table.
- Use identifier to define which rows of two tables can be matched.



# LEFT JOIN example
```postgresql
SELECT *
FROM renting_selected AS r
LEFT JOIN customers_selected AS c
ON r.customer_id = c.customer_id;
```



# More than one JOIN
```postgresql
SELECT m.title,
	c.name
FROM renting AS r
LEFT JOIN movies AS m
ON r.movie_id = m.movie_id
LEFT JOIN customers AS c
ON r.customer_id = c.customer_id;
```






















