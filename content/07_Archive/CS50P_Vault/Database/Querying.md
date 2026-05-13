

----

# Querying

## Keywords

- SELECT  —> Indicates which fields should be selected
- FROM —> Indicates the tables in which these fields are located.
- COUNT() —> Returns the number of records with a value in a field
    
    **COUNT() 1 FIELD**
    
    ```sql
    SELECT COUNT(birthdate) AS count_birthdates
    FROM people;
    
    # Use alias for clarity
    # |count_birthdates|
    # |----------------|
    # |6152            |
    
    ```
    
    ---
    
    **COUNT() MULTIPLE FIELDS**
    
    ```sql
    SELECT COUNT(name) AS count_names, COUNT(birthdate) AS count_birthdates
    FROM people;
    
    # |count_names|count_birthdates|
    # |-----------|----------------|
    # |6397       |                |
    ```
    
    ---
    
    **USING * WITH COUNT()**
    
    - Counts record in table
    
    ```sql
    SELECT COUNT(*) AS total_records
    FROM people;
    
    # |total_records|
    # |-------------|
    # |8397         |
    ```
    
    ---
    
- DISTINCT —> Select all the unique values from a field
    - Removes Duplicates to Return Only Unique Values
    
    ```sql
    SELECT language
    FROM films;
    
    # |language|
    # |--------|
    # |Danish  |
    # |Danish  |
    # |Greek   |
    # |Greek   |
    # |Greek   |
    ```
    
    ---
    
    ```sql
    SELECT DISTINCT language
    FROM films;
    
    # |language|
    # |--------|
    # |Danish  |
    # |Greek   |
    ```
    
    ---
    
- COUNT() with DISTINCT —> Common way to count the number of unique values in a field.
    - Combine COUNT() with DISTINCT to count unique values
    
    ```sql
    SELECT COUNT(DISTINCT bithdate) AS count_distinct_birthdates
    FROM people;
    
    # |count_distinct_birthdates|
    # |-------------------------|
    # |5398                     |
    ```
    
    ---
    
- LIMIT —> Limits how many results we return
    
    ```sql
    SELECT name
    FROM people
    LIMIT 10;
    ```
    
    ---
    
- WHERE —> Filtering
    - Focus on only the data relevant to your questions.
    
    ```sql
    WHERE color = 'green'
    ```
    
    ## **WHERE with Comparison Operators**
    
    ```sql
    SELECT title
    FROM films
    WHERE release_year > 1960:
    
    # |title                 |
    # |----------------------|
    # |Judgement at Nuremberg|
    # |Pocketful of Miracles |
    # |The Hustler           |
    # |The Misfits           |
    ```
    
    ## Comparison Operators
    
    ```sql
    SELECT title
    FROM films
    WHERE release_year < 1960:
    
    # |title                                          |
    # |-----------------------------------------------|
    # |Intolerance:Love's Struggle Throughout the Ages|
    # |Over the Hill to the Poorhouse                 |
    # |The Big Parade                                 |
    # |Metroplis                                      |
    ```
    
    ```sql
    SELECT title
    FROM films
    WHERE release_year <= 1960:
    
    # |title                                          |
    # |-----------------------------------------------|
    # |Intolerance:Love's Struggle Throughout the Ages|
    # |Over the Hill to the Poorhouse                 |
    # |The Big Parade                                 |
    # |Metroplis                                      |
    ```
    
    ```sql
    SELECT title
    FROM films
    WHERE release_year = 1960:
    
    # |title        |
    # |-------------|
    # |Elmer Gantry |
    # |Psycho       |
    # |The Apartment|
    ```
    
    ```sql
    SELECT title
    FROM films
    WHERE release_year <> 1960:
    
    # Show not equal to 1960
    
    # |title                                          |
    # |-----------------------------------------------|
    # |Intolerance:Love's Struggle Throughout the Ages|
    # |Over the Hill to the Poorhouse                 |
    # |The Big Parade                                 |
    # |Metroplis                                      |
    ```
    
    ---
    
    ## WHERE with Strings
    
    ```sql
    SELECT title
    FROM films
    WHERE country = 'Japan';
    
    # |title            |
    # |-----------------|
    # |Seven Samurai    |
    # |Tora! Tora! Tora!|
    # |Akira            |
    # |Madadayo         |
    # |Street Fighter   |
    ```
    

## Selecting Multiple fields

- We can list multiple field names after the SELECT keyword, separated by commas.
- Example: we can select 3 fields such as name, card_num and total_fine
    - SELECT name, card_num, total_fine FROM table
    - OR
    - SELECT * FROM table

## Aliasing

- Aliases are declared in the SELECT Statement
- Sometimes it can be helpful to rename columns in our result set
- We can do this using aliasing
- Example:
    - Perhaps we'd like to select the name and hire year for each record in the employees table.
    - We could alias the name column as first_name in the query by adding the AS keyword to indicate an alias of first_name after selecting the name field.
- The alias only applies to the result of this particular query; in other words, the field name in the employees table itself is still name rather than first_name.

## Selecting Distinct Records

- Some SQL questions require a way to return a list of unique values
- Example:
    - Imagine that we are interested in getting a list of years in which we hired our current employees.
    - We select the year_hired field from the employees table, the result set shows several years listed twice
    - To get a list of years with no repeat values, we can add the DISTINCT keyword before the year_hired field name in the SELECT statement
    - SELECT DISTINCT year_hired FROM table

## DISTINCT With Multiple Fields

- It's possible to return the unique combinations of multiple field values by listing multiple fields after the DISTINCT keyword.
- EXAMPLE:
    - SELECT DISTINCT dept_id, year_hired FROM employees;

## Views

- A view refers to a table that is the result of a saved SQL SELECT statement.
- Views are considered virtual tables, which means that the data a view contains is not generally stored in the database.
- A benefit of this is that whenever the view is accessed, it automatically updates the query results to account for any updates to the underlying database.

- To create a view, we'll add a line of code before the SELECT statement: CREATE VIEW, then the name we'd like for the new view.
- Then the AS keyword to assign the results of the query to the new view name.

- EXAMPLE:
    - CREATE VIEW employee_hire_years AS
    - SELECT id, name, year_hired
    - FROM employees;

---