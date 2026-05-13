

# Adding and subtracting date / time data
```postgresql
SELECT date '2005-09-11' - date '2005-09-10';
```

```postgresql
SELECT date '2005-09-11 00:00:00' - date '2005-09-09 12:00:00';
```
- returns: 1 day 12:00:00


# Calculating time periods with AGE
```postgresql
SELECT AGE(timestamp '2005-09-11 00:00:00', timestamp '2005-09-09 12:00:00');
```



# Example
```postgresql
SELECT 
	AGE(rental_date)
FROM rental;
```

```postgresql
+-----------------------------------+
| age                               |
| 13 years 11 mons 12 days 01:06:30 |
| 13 years 11 mons 12 days 01:05:27 |
| 13 years 11 mons 12 days 00:56:21 |
+-----------------------------------+
```


# Date / time arithmetic using INTERVALs
```postgresql
SELECT timestamp '2019-05-01' + 21 * INTERVAL '1 day';
```

```postgresql
+-----------------------------+
| timestamp without timezone  |
|-----------------------------|
| 2019-05-22 00:00:00         |
+-----------------------------+
```


























































