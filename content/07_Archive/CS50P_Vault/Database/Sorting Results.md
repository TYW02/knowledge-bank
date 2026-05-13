
----

# ORDER BY

```sql
SELECT title, budget
FROM films
ORDER BY budget;

# |title               |budget|
# |--------------------|------|
# |Tarnation           |218   |
# |My Dtae With Drew   |1100  |
# |A Plague So Pleasant|1400  |
# |The Mongol King     |3250  |
```

```sql
SELECT title, budget
FROM films
ORDER BY title;

# |title                     |budget  |
# |--------------------------|--------|
# |#Horror                   |1500000 |
# |10 Cloverfield Lane       |15000000|
# |10 Dyas in a Madhouse     |12000000|
# |10 Things I Hate About You|16000000|
```

## ASCending

```sql
SELECT title, budget
FROM films
ORDER BY budget ASC;

# |title               |budget|
# |--------------------|------|
# |Tarnation           |218   |
# |My Date With Drew   |1100  |
# |A Plague So Pleasant|1400  |
# |The Mongol King     |3250  |
```

## DESCending

```sql
SELECT title, budget
FROM films
ORDER BY budget DESC;

# |title                         |budget|
# |------------------------------|------|
# |Love and Death on Long Island |null  | 
# |The Chambermaid on the Titanic|null  |
# |51 Birch Street               |null  |
```

```sql
SELECT title, budget
FROM films
WHERE budget IS NOT NULL
ORDER BY budget DESC;

# |title            |budget     | 
# |-----------------|-----------|
# |The Host         |12215500000|
# |Lady Vengeance   |4200000000 |
```

# Sorting Fields

![Untitled](Untitled%2021.png)

# ORDER BY multiple fields

- ORDER BY field_one, field_two
- Think of field_two as a tie-breaker when the first field is not decisive in telling the order
    - E.g. sort by Oscar wins but get tie, we can break tie by adding a second condition

![Untitled](Untitled%2022.png)

# DIFFERENT ORDERS

- We are sorting birth-date in ascending order and name in descending order

![Untitled](Untitled%2023.png)

# Order of Execution

1. FROM
2. WHERE
3. SELECT
4. ORDER BY
5. LIMIT