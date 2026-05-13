



----

# GROUP BY single fields

```sql
SELECT certification, COUNT(title) AS title_count
FROM films
GROUP BY certification;

# |certification|title_count|
# |-------------|-----------|
# |Unrated      |62         |
# |M            |5          |
# |G            |112        |
# |NC-17        |7          |
```

# Error Handling

![Untitled](Untitled%2024.png)

# GROUP BY multiple fields

```sql
SELECT certification, language, COUNT(title) AS title_count
FROM films
GROUP BY certification, language;

# |certification|language |title_count|
# |-------------|---------|-----------|
# |null         |null     |5          |
# |Unrated      |Japanese |2          |
# |R            |Norwegian|2          |
```

# GROUP BY with ORDER BY

![Untitled](Untitled%2025.png)

# Order Of Execution

1. FROM 
2. GROUP
3. SELECT
4. ALIAS
5. SORT
6. LIMIT