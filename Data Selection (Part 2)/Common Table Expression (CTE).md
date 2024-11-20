# Common Table Expressions (CTE)

Sometimes we have queries that are so complicated that even using subqueries doesn’t help much. In this cases Common Table Expressions can significantly make a life of a data analyst easier.

<aside>

📖 **Common Table Expression (CTE)** **→** is a temporary result set that you can define in a query

</aside>

*CTEs* make complex queries easier to read and maintain by breaking them into smaller, manageable parts. They are defined using the `WITH` keyword.

<aside>

💡 **CTEs** are often used as an alternative to subqueries 

</aside>

# CTE Logic 🧩

- A *CTE* is like a temporary view that exists only for the duration of the query.
- It improves query readability by allowing you to structure a query in logical steps.
- You can reference the *CTE* multiple times within the same query, eliminating the need to repeat complex subqueries.

<aside>

💡 The expression `WITH` is considered *"temporary"* because the result is not stored permanently in the database schema. It acts as a temporary representation that exists only during the execution of the query.

It is valid only within the query to which it belongs, allowing for improved query structure without cluttering the global namespace.

</aside>

# CTE Example 🧪

Before looking at an example, let’s have a look at *CTE syntax*:

```sql
WITH cte_name (optional_column_names) AS (
    SELECT query
)

SELECT columns
FROM cte_name;
```

Usually, we have the following steps:

1. Introduce the `WITH` clause.
2. Specify the name of the `CTE`.
3. Optionally: define the names for the columns of the resulting table, separated by commas.
4. Introduce `AS` followed by the subquery, the result of which can be used in other parts of the SQL query, using the name defined in step 2.
5. Optionally: if multiple *CTEs* are needed, a comma is added, and steps 2-4 are repeated.

let’s create a summary table of flights of *“Lufthansa”* air company:

```sql
-- example of using the WITH clause
WITH lufthansa_trips AS (
    SELECT *
    FROM flight f
    INNER JOIN aircompany ac ON f.air_company_id = ac.id WHERE ac.name = "Lufthansa"
)

SELECT plane_name, COUNT(plane_name) AS plane_count
FROM lufthansa_trips 
GROUP BY plane_name;
```

# Advantages ⚡

- **Improved Readability**:
    - CTEs break down complex queries into named steps, making SQL easier to understand and maintain.
- **Reusability**:
    - You can define complex logic once in a CTE and reuse it in multiple parts of the query.

# Important Notes ⚠️

- **SQL Dialect Compatibility**:
    - Not all SQL databases support *CTEs* n the same way, so be sure to check the capabilities of your database.
- **Temporary Scope**:
    - CTEs are only valid within the query where they’re defined, so they cannot be reused across different queries