

# Main types
date
- YYYY-MM-DD
- example: 2018-12-30
timestamp
- YYYY-MM-DD HH:MM:SS
- example: 2018-12-30 13:10:04.3




# Date/time format examples

### 1pm on January 10, 2018

01/10/18 1:00
10/01/18 01:00:00
01/10/2018 1pm
January 10th, 2018 1pm
10 Jan 2018 1:00
01/10/18 01:00:00


# ISO 8601
ISO = International Organization for Standards
YYYY-MM-DD HH:MM:SS
Example: 2018-01-05 09:35:15



# UTC and timezones
UTC = Coordinated Universal Time

Timestamp with timezone:
YYYY-MM-DD HH:MM:SS
Example: 2004-10-19 10:23:54+02



# Date and time comparisons

Compare with > , <, =
```postgresql
SELECT '2018-01-01' > '2017-12-31';
```

now(): current timestamp
```postgresql
SELECT now() > '2017-12-31';
```


# Date addition
```postgresql
SELECT '2010-01-01'::date + 1;
```

```postgresql
SELECT '2018-12-10'::date + '1 year'::interval;
```

```postgresql
SELECT '2018-12-10'::date + '1 year 2 days 3 minutes'::interval;
```




























































