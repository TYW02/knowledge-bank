#Insert

## What's a Schema ?
We previously described a table in a database as a two-dimensional set of rows and columns, with the columns being the properties and the rows being instances of the entity in the table. 

In SQL, the _database schema_ is what describes the structure of each table, and the datatypes that each column of the table can contain.

For example, in our **Movies** table, the values in the _Year_ column must be an Integer, and the values in the _Title_ column must be a String.



## Inserting new Data
When inserting data into a database, we need to use an `INSERT` statement, which declares which table to write into, the columns of data that we are filling, and one or more rows of data to insert. 

In general, each row of data you insert should contain values for every corresponding column in the table. You can insert multiple rows at a time by just listing them sequentially.
```sql
INSERT INTO mytable 
VALUES (value_or_expr, another_value_or_expr, …), (value_or_expr_2, another_value_or_expr_2, …), …;
```

In some cases, if you have incomplete data and the table contains columns that support default values, you can insert rows with only the columns of data you have by specifying them explicitly.
```sql
INSERT INTO mytable
(column, another_column, …) 
VALUES (value_or_expr, another_value_or_expr, …), 
	(value_or_expr_2, another_value_or_expr_2, …), 
…;
```


In these cases, the number of values need to match the number of columns specified. Despite this being a more verbose statement to write, inserting values this way has the benefit of being forward compatible. For example, if you add a new column to the table with a default value, no hardcoded `INSERT` statements will have to change as a result to accommodate that change.

In addition, you can use mathematical and string expressions with the values that you are inserting.  
This can be useful to ensure that all data inserted is formatted a certain way.
```sql
INSERT INTO boxoffice 
(movie_id, rating, sales_in_millions) 
VALUES (1, 9.9, 283742034 / 1000000);
```

























































