
# SQL Injection

> [!Question] 
> To extract the column names of a table called "users" via UNION injection, which table should you query ?
> - A) `information_schema.tables`
> - B) `information_schema.columns`
> - C) `information_schema.users`
> - D) `mysql.user`
> 
> > [!Answer]-
> >- **B**
> > - To get the column names inside a **specific table** you need `information_schema.columns` filtered by `table_name='users'`




























































