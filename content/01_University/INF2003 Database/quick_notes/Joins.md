

# INNER JOIN

> [!Important] Syntax (Pattern to Remember)
> ```SQL
> FROM tableA JOIN tableB ON tableA.key = tableB.key
> ```

> [!error] What I thought it was
> ```SQL
> SELECT customer_name, order_date 
> FROM customers INNER JOIN 
> customers.customer_id ON orders.customer_id;
> ```

> [!success] Correct Version
> ```SQL
> SELECT customers.customer_name, orders.order_date
> FROM customers INNER JOIN orders
> ON customers.customer_id = orders.customer_id;
> ```






































