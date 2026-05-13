

# User-defined data types

### Enumerated data types
```postgresql
CREATE TYPE dayofweek AS ENUM(
	'Monday',
	'Tuesday',
	'Wednesday',
	'Thursday',
	'Friday',
	'Saturday',
	'Sunday'
);
```


# Getting information about user-defined data types

```postgresql
SELECT typname, typcategory
FROM pg_type
WHERE typname='dayofweek';
```

```postgresql
+------------------+-------------------+
| typname          | typcategory       |
|------------------|-------------------|
| dayofweek        | E                 |
+------------------+-------------------+
```



# Getting information about user-defined data types
```postgresql
SELECT column_name, data_type, udt_name
FROM INFORMATION_SCHEMA.COLUMNS
WHERE table_name = 'film';
```

![[Pasted image 20230123140307.png]]



# User-defined functions
```postgresql
CREATE FUNCTION squared(i interger) RETURN integer AS $$
	BEGIN
		RETURN i * i;
	END;
$$ LANGUAGE plpgsql
```

```postgresql
SELECT squared(10);
```



































