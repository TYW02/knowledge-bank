

# Column constraints
- Foreign key: value that exists in the referenced column, or NULL
- Primary key: unique, not NULL
- Unique: values must all be different except for NULL
- Not null: NULL not allowed: must have a value
- Check constraints: conditions on the value
	- column1 > 0
	- columnA > columnB




# Data types
| Common    | Special         |
| --------- | --------------- |
| Numeric   | Arrays          |
| Character | Monetary        |
| Date/Time | Binary          |
| Boolean   | Geometric       |
|           | Network Address |
|           | XML             |
|           | JSON            |
|           | and more !                |



# Casting with CAST()
Format
```postgresql
-- With the CAST function
SELECT CAST(value AS new_type);
```

### Examples
```postgresql
-- Cast 3.7 as an integer
SELECT CAST(3.7 AS integer);
```

```postgresql
-- Cast a column called total as an integer
SELECT CAST(total AS interger)
	FROM prices;
```




# Casting with ::
Format
```postgresql
-- With :: notation
SELECT value::new_type;
```

### Examples
```postgresql
-- Cast 3.7 as an integer
SELECT 3.7::integer;
```

```postgresql
SELECT total::integer
	FROM prices;
```












































