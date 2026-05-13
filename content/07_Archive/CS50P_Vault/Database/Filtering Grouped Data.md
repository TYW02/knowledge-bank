


----

# HAVING

```sql
SELECT release_year, COUNT(title) AS title_count
FROM films
GROUP BY release_year
HAVING COUNT(title) > 10;

# |release_year|title_count|
# |------------|-----------|
# |1988        |31         |
# |null        |42         |
# |2008        |225        |
```

---

# Order Of Execution

1. FROM
2. WHERE
3. GROUP BY
4. HAVING 
5. SELECT ORDER BY
6. LIMIT

- We can see `WHERE` is executed before `GROUP BY` and before any aggregation occurs.
- This order is also why we cannot use the alias with `HAVING,` but we can with `ORDER BY.`

# HAVING VS WHERE

- `WHERE` filters individual records while `HAVING` filters grouped records.

### **WHERE (What films were released in the year 2000?)**

```sql
SELECT title
FROM films
WHERE release_year = 2000;

# |title         |
# |--------------|
# |102 Dalmatians|
# |28 Days       |
```

### HAVING (In what years was the average film duration over two hours?)

```sql
SELECT release_year
FROM films
GROUP BY release_year
HAVING AVG(duration) > 120;
```