
# Arithmetic

- `+`
- `-`
- `*`
- `/`

### Example

```sql
SELECT (4 + 3);

# |7|

SELECT (4 * 3);
# |12|

SELECT (4 - 3);
# |1|

SELECT (4 / 3);
# |1|
```

# Aggregate VS Arithmetic

- Aggregate functions perform their operations on the fields vertically
- Arithmetic adds up the records horizontally

![Untitled](Untitled%2015.png)

# Aliasing with Arithmetic

```sql
SELECT (gross - budget) AS profit
FROM films;

# |profit  |
# |--------|
# |null    |
# |2900000 |
# |null    |
```

# Aliasing with Functions

```sql
SELECT MAX(budget) AS max_budget, MAX(duration) AS max_duration
FROM films;

# |max_budget |max_duration|
# |-----------|------------|
# |12215500000|334         |
```

## Order Of Execution

- Step 1: `FROM`
- Step 2: `WHERE`
- Step 3: `SELECT` (aliases are defined here)
- Step 4: `LIMIT`

- Aliases defined in the `SELECT` clause cannot be used in the `WHERE` clause due to order of execution

