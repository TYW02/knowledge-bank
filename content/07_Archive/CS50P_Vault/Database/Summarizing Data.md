



----

# Aggregate Function

- Count()
- AVG()
    
    ```sql
    SELECT AVG(budget)
    FROM films;
    
    # |avg             |
    # |----------------|
    # |39902826.2684...|
    ```
    
- SUM()
    
    ```sql
    SELECT SUM(budget)
    FROM films;
    
    # |sum         |
    # |------------|
    # |181079025606|
    ```
    
- MIN()
    
    ```sql
    SELECT MIN(budget)
    FROM films;
    
    # |min|
    # |---|
    # |218|
    ```
    
- MAX()
    
    ```sql
    SELECT MAX(budget)
    FROM films;
    
    # |max        |
    # |-----------|
    # |12215500000|
    ```
    

## Non-Numerical Data

---

### Numerical Fields Only

- AVG()
- SUM()

### Various Data Types

- COUNT()
- MIN()
- MAX()

## MIN()  ↔   MAX()

Minimum ↔ Maximum

Lowest ↔ Highest

A ↔ Z

1715 ↔ 2022

0 ↔ 100

### EXAMPLE

```sql
SELECT MIN(country)
FROM films;

# |min        |
# |-----------|
# |Afghanistan|
```

```sql
SELECT MAX(country)
FROM films;

# |max         |
# |------------|
# |West Germany|
```

## Aliasing When Summarizing

```sql
SELECT MIN(country) AS min_country
FROM films;

# |min_country|
# |-----------|
# |Afghanistan|
```

# Using WHERE with aggregate functions

```sql
SELECT AVG(budget) AS avg_budget
FROM films
WHERE release_year >= 2010;

# |avg_budget          |
# |--------------------|
# |41072235.18324607...|
```

```sql
SELECT SUM(budget) AS sum_budget
FROM films
WHERE release_year = 2010;

# |sum_budget|
# |----------|
# |8942365000|
```

```sql
SELECT MIN(budget) AS min_budget
FROM films
WHERE release_year = 2010;

# |min_budget|
# |----------|
# |65000     |
```

```sql
SELECT MAX(budget) AS max_budget
FROM films
WHERE release_year = 2010;

# |max_budget|
# |----------|
# |6000000000|
```

```sql
SELECT COUNT(budget) AS count_budget
FROM films
WHERE release_year = 2010;

# |count_budget|
# |------------|
# |194         |
```

# ROUND()

- Round a number to a specified decimal

`ROUND(number_to_round, decimal_places)`

```sql
SELECT AVG(budget) AS avg_budget
FROM files
WHERE release_year >= 2010;

# |avg_budget          |
# |--------------------|
# |41072235.18324607...|
```

```sql
SELECT ROUND(AVG(budget), 2) AS avg_budget
FROM films
WHERE release_year >= 2010;

# |avg_budget |
# |-----------|
# |41072235.18|
```

```sql
SELECT ROUND(AVG(budget), -5) AS avg_budget
FROM films
WHERE release_year >= 2010;

# |avg_budget|
# |----------|
# |41100000  |
```

- Function rounds to the left of the decimal point instead of the right.
- Using -5 will round to the hundred thousand or five places to the left