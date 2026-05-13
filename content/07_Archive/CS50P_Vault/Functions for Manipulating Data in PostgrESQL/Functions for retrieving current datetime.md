

# Retrieving the current timestamp
```postgresql
SELECT NOW();
```

```postgresql
+-------------------------------+
| now()                         |
|-------------------------------|
| 2019-04-19 02:51:18.448641+00 |
+-------------------------------+
```


## PostgreSQL specific casting
```postgresQl
SELECT NOW()::timestamp;
```

## CAST() function
```postgresql
SELECT CAST(NOW() as timestamp);
```



# Retrieving the current timestamp
```postgresql
SELECT CURRENT_TIMESTAMP;
```

```postgresql
+---------------------------------+
| current_timestamp               |
|---------------------------------|
| 2019-04-19 02:51:18.448641+00   |
+---------------------------------+
```


```postgresql
SELECT CURRENT_TIMESTAMP(2);
```

```postgresql
+---------------------------------+
| current_timestamp               |
|---------------------------------|
| 2019-04-19 02:51:18.44+00       |
+---------------------------------+
```



# Current date and time
```postgresql
SELECT CURRENT_DATE;
```

```postgresql
+---------------+
| current_date  |
|---------------|
| 2019-04-19    |
+---------------+
```


```postgresql
SELECT CURRENT_TIME;
```

```postgresql
+-------------------------+
| current_time            |
|-------------------------|
| 04:06:30.929845+00:00   |
+-------------------------+
```























