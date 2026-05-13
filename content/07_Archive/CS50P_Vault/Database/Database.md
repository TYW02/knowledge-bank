

----

# Databases

- A database stores data.

![Untitled](07_Archive/CS50P_Vault/Database/_assets_/Untitled.png)

## Relational Databases

- Define relationships between tables of data inside the database

## Database Advantages

- More Storage than spreadsheet applications
- Storage is more secure
- Many users can write query to gather insights at the same time.

## SQL

- Widely Used
- Creating
- Querying
- Updating
- Relational Database

---

---

# Tables

- Organized into rows and columns
- Rows are often referred to as records and columns as fields
- Name should be lowercase
- Name should not include space
- Ideally refer to a collective group e.g. (inventory)

## Records

- A Record is a row in a table
- Holds data on an individual observation

## Field

- A Field is a column in a table.
- Hold 1 piece of information about all observations in the table
- E.g. ‘name’ field in the patrons table lists all of the names of our library patrons

- Generally, field names should be lowercase and should not involve spaces.
- A field name should be singular rather than plural because it refers to the information contained in that field for a single record.

## Key

- A unique identifier
- Unique value which identifies a record so that it can be distinguished from other records in the same table

---

---

# Order Of Execution

- SQL code is not processed in order it is written.

```sql
# 2 SELECT name
# 1 FROM people
# 3 LIMIT 10;
```

- Good to know processing order for debugging and aliasing
- Aliases are declared in the SELECT Statement

```sql
--- Written Code:
#3 SELECT item
#1 FROM coats
#2 WHERE color = 'green'
#4 LIMIT 5;
```

---

---

# Multiple Criteria

- OR
    - Use OR when you need to satisfy at least one condition
    
    ```sql
    SELECT title
    FROM films
    WHERE release_year = 1994
    OR release_year = 2000;
    
    # |title                    |
    # |-------------------------|
    # |3 Ninjas Kick Back       |
    # |A Low Down Dirty Shame   |
    # |Ace Ventura:Pet Detective|
    ```
    
- AND
    - Use AND if we need to satisfy all criteria
    
    ```sql
    SELECT title 
    FROM films
    WHERE release_year > 1994
    AND release_year < 2000;
    
    # |title                         |
    # |------------------------------|
    # |Ace Ventura: When Nature Calls|
    # |Apollo 13                     |
    # |Assassins                     |
    # |Babe                          |
    ```
    
- BETWEEN
    
    ```sql
    SELECT title 
    FROM films
    WHERE release_year 
    BETWEEN 1994 AND 2000;
    
    # |title                     |
    # |--------------------------|
    # |3 Ninjas Kick Back        |
    # |A Low Down Dirty Shame    |
    # |Ace Venture: Pet Detective|
    # |Baby's Day Out            |
    ```
    
- AND, OR EXAMPLE
    
    ```sql
    SELECT title
    FROM films
    WHERE (release_year = 1994 OR release_year = 1995)
    AND (certification = 'PG' OR certification = 'R')
    
    # |title                 |
    # |----------------------|
    # |3 Ninjas Kick Back    |
    # |A Low Down Dirty Shame|
    # |Baby's Day Out        |
    # |Beverly Hills Cop III |
    ```
    
- BETWEEN, AND, OR
    
    ```sql
    SELECT title
    FROM films
    WHERE release_year
    BETWEEN 1994 AND 2000 AND country='UK';
    
    # |title                      |
    # |---------------------------|
    # |Four Weddings and a Funeral|
    # |The Hudsucker Proxy        |
    # |Dead Man Walking           |
    # |GoldenEye                  |
    ```
    

```sql
SELECT *
FROM coats
WHERE color = 'yellow' OR length = 'short';
```

```sql
SELECT *
FROM coats
WHERE color = 'yellow' AND length = 'short';
```

```sql
SELECT *
FROM coats
WHERE buttons BETWEEN 1 AND 5;
```

![Untitled](07_Archive/CS50P_Vault/Database/_assets_/Untitled%201.png)

![Untitled](07_Archive/CS50P_Vault/Database/_assets_/Untitled%202.png)

---

---

# Filtering Text

- WHERE can also filter text

![Untitled](07_Archive/CS50P_Vault/Database/_assets_/Untitled%203.png)

- Filter a pattern rather than specific text
- LIKE
    - Used to search for a pattern in a field
    
    ![Untitled](07_Archive/CS50P_Vault/Database/_assets_/Untitled%204.png)
    
- NOT LIKE
    
    ![Untitled](07_Archive/CS50P_Vault/Database/_assets_/Untitled%205.png)
    
- IN

---

## Wildcard Position

![Untitled](07_Archive/CS50P_Vault/Database/_assets_/Untitled%206.png)

---

---

# NULL

- Missing value
    - Human Error
    - Information Not Available
    - Unknown

![Untitled](Untitled%207.png)

## IS NULL

![Untitled](Untitled%208.png)

## IS NOT NULL

![Untitled](Untitled%209.png)

## COUNT() vs IS NOT NULL

![Untitled](Untitled%2010.png)

# NULL Summary

![Untitled](Untitled%2011.png)

---

---

# Summarizing Data

<aside>
🍻 [Summarizing Data](Summarizing%20Data%20a5f2f105ee364049b847aba986a9c95d.md)

</aside>

---

---

# Aliasing and Arithmetic

<aside>
➗ [Aliasing and Arithmetic](Aliasing%20and%20Arithmetic%20f02dcc29be1240f88bbd0f10b1b37ad0.md)

</aside>

---

---

# Sorting Results

<aside>
⛵ [Sorting Results](Sorting%20Results%20092b7333be124238a56a8a0f43c2ac47.md)

</aside>

---

---

# Grouping Data

<aside>
👥 [Grouping Data](Grouping%20Data%203a0a6c0cf8654b6c8756c4976d5beb94.md)

</aside>

---

# Filtering Grouped Data

<aside>
🎢 [Filtering Grouped Data](Filtering%20Grouped%20Data%206f24b54e9e9949dc80562d86cbbd9eb2.md)

</aside>

# LIST OF PAGES

---

[SQL Formatting](SQL%20Formatting.md)

[Debugging SQL](Debugging%20SQL.md)

[SQL Flavors](SQL%20Flavors.md)

[Data Types](Data%20Types.md)

[Querying](Querying.md)

---

[Summarizing Data](Summarizing%20Data.md)

[Aliasing and Arithmetic](Aliasing%20and%20Arithmetic.md)

[Sorting Results](Sorting%20Results.md)

[Grouping Data](Grouping%20Data.md)

[Filtering Grouped Data](Filtering%20Grouped%20Data.md)