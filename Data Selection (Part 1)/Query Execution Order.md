# Query Execution Order ➡️

It turns out that when we write queries in SQL and execute them, something strange happens 🕵️‍♂️

<aside>

💡 SQL queries aren’t executed in the order they are written!

</aside>

Instead, SQL engines process queries according to a specific *execution order* that might look a little backward at first glance. This order is essential to how SQL *retrieves*, *filters* and *organizes* data efficiently. The below picture describes how a query is usually executed by SQL:

![sql-query-execution-order.png](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/Data%20Selection%20(Part%201)/img/sql-query-execution-order.png)

We see that although we write `SELECT` operator the first, it’s executed by SQL almost at the end. Let’s look at the query execution in details:

- *FROM —* First, SQL decides where to pull the data from. This includes the tables you specify and any joins if you’re combining data from multiple sources.
- *WHERE —* Next, SQL applies any row-level filters specified in the `WHERE` clause. This step ensures only rows meeting these conditions are processed in the next steps.
- *GROUP BY —* After filtering rows, SQL groups the remaining data according to the specified columns. This allows for grouping-based calculations, like counting rows in each department.
- *HAVING —* Now, SQL filters these groups based on conditions set in the `HAVING` clause. It’s like `WHERE` but for grouped data, making it useful for conditions on aggregated results.
- *SELECT —* Finally, SQL retrieves the specified columns and evaluates any aggregate functions, calculated fields, or aliases you defined in `SELECT`.
- *ORDER BY —* The result set is then sorted according to the `ORDER BY` clause, allowing you to arrange it in ascending or descending order.
- *LIMIT —* If there’s a limit, SQL applies it last, showing only the specified number of rows.

It’s a bit of a hidden mystery in SQL! This execution order is crucial to understand for writing efficient queries, as each clause depends on the processing of the previous ones. The next time you run a query, remember that the SQL engine is busy unraveling each clause step-by-step, even if it feels out of order!