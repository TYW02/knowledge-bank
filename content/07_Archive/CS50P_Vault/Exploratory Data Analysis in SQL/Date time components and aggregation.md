

# Common date/time fields

### Fields
- Century: 2019-01-01 = century 21
- Decade: 2019-01-01 = decade 201
- year, month, day
- hour, minute, second
- week
- dow: day of week



# Extracting fields
```postgresql
-- functions to extract datetime fields

date_part('field', timestamp)

EXTRACT(FIELD FROM timestamp)
```

```postgresql
-- now is 2019-01-08 22:15:10.647281-06

SELECT date_part('month', now())
EXTRACT(MONTH FROM now());
```




# Extract to summarize by field

### Individual sales
```postgresql
SELECT *
FROM sales
WHERE date >= '2010-01-01'
	AND date < '2017-01-01''
```

### By Month
```postgresql
SELECT date_part('month', date)
AS month,
sum(amt)
FROM sales
GROUP BY month
ORDER BY month;
```


# Truncating dates
```postgresql
date_trunc('field', timestamp)
```

```postgresql
-- now() is 2018-12-17 21:45:15.6829-06

SELECT date_trunc('month', now());
```



# Truncate to keep larger unit

### Individual sales
```postgresql
SELECT *
	FROM sales
WHERE date >= '2017-06-01'
	AND date < '2019-02-01';
```

### By month with year
```postgresql
SELECT date_trunc('month', date)
	AS month
	sum(amt)
	FROM sales
GROUP BY month
ORDER BY month;
```






















































