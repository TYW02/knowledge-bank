
As your data changes over time, SQL provides a way for you to update your corresponding tables and database schemas by using the `ALTER TABLE` statement to add, remove, or modify columns and table constraints.


## Adding Columns
The syntax for adding a new column is similar to the syntax when creating new rows in the `CREATE TABLE` statement. You need to specify the data type of the column along with any potential table constraints and default values to be applied to both existing _and_ new rows. In some databases like MySQL, you can even specify where to insert the new column using the `FIRST` or `AFTER` clauses, though this is not a standard feature.
```sql
ALTER TABLE mytable 
ADD column DataType OptionalTableConstraint
	DEFAULT default_value;
```



## Removing Columns
Dropping columns is as easy as specifying the column to drop, however, some databases (including SQLite) don't support this feature. Instead you may have to create a new table and migrate the data over.
```sql
ALTER TABLE mytable 
DROP column_to_be_deleted;
```


## Renaming the table
If you need to rename the table itself, you can also do that using the `RENAME TO` clause of the statement.
```sql
ALTER TABLE mytable 
RENAME TO new_table_name;
```


## Other Changes
Each database implementation supports different methods of altering their tables, so it's always best to consult your database docs before proceeding: [MySQL](https://dev.mysql.com/doc/refman/5.6/en/alter-table.html "MySQL Alter Table"), [Postgres](http://www.postgresql.org/docs/9.4/static/sql-altertable.html "Postgres Alter Table"), [SQLite](https://www.sqlite.org/lang_altertable.html "SQLite Alter Table"), [Microsoft SQL Server](https://msdn.microsoft.com/en-us/library/ms190273.aspx "Microsoft SQL Server Alter Table").









































