

# TIMESTAMP data types
- ISO 8601 format: yyyy-mm-dd
```postgresql
+---------------------------------+
| timestamp                       |
| 2019-03-26 01:05:17.93027+00    |
+---------------------------------+
```

```postgresql
SELECT payment_date
FROM payment;
```

```postgresql
+---------------------------------+
| payment_date                    |
| 2005-05-25 11:30:37             |
+---------------------------------+
```



# DATE and TIME data types
```postgresql
+-------------+--------------------+
| date        | time               |
|-------------|--------------------|
| 2005-05-28  | 01:05:17.93027+00  |
+-------------+--------------------+
```

```postgresql
SELECT create_date
FROM customer
```

```postgresql
+------------+
| create_date|
|------------|
| 2006-02-14 |
+------------+
```


# INTERVAL data types
```postgresql
+----------+
| interval |
|----------|
| 4 days   |
+----------+
```

```postgresql
SELCT rental_date + INERVAL '3 days' as expected_return
FROM rental;
```

```postgresql
+--------------------+
| expected_return    |
|--------------------|
| 2005-05-27 22:53:30|
+--------------------+
```


# Looking at date and time types
```postgresql
SELECT
	column_name,
	data_type
FROM INFORMATION_SCHEMA.COLUMNS
WHERE column_name IN ('rental_date')
	AND table_name = 'rental';
```

```postgresql
+-------------+-------------------------------+
| column_name | data_type                     |
|-------------|-------------------------------|
| rental_date | timestamp without time zone   |
+-------------+-------------------------------+
```



















