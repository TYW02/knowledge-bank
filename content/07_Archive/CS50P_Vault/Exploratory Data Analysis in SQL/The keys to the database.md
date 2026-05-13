

# Foreign keys
- Reference another row
	- In a different table or the same table
	- Via a unique ID
		- Primary key column containing unique, non-NULL values
	- Values restricted to values in referenced column OR NULL




# Coalesce Function
```postgresql
coalesce(value_1, value_2 [,...])
```
- Operates row by row
- Returns first non-NULL value


```postgresql
SELECT *
	FROM prices;
```

```postgresql
column_1 | column_2
---------+---------
		 |	10
         |
      22 |
       3 |   4
```

```postgresql
SELECT coalesce(column_1, column_2)
	FROM prices;
```

```postgresql
coalesce
------------
	10

	22
	3
```













































































