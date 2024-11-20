# IF Operator ⚖️

The `IF` operator in SQL is used to execute conditional logic within queries. While SQL itself doesn’t have a direct `IF` statement like traditional programming languages, the functionality can be achieved using the `CASE` statement or specific database functions, depending on the SQL dialect you are using.

<aside>

📖 `IF` — is a conditional function that allows performing conditional logic within queries

</aside>

It's particularly useful for returning specific values based on whether a condition is *true* or *false*. While not part of standard SQL, some database systems like MySQL and SQL Server support the `IF` function.

# IF Logic 🧩

- The `IF` operator evaluates a condition and returns one value if the condition is true and another value if the condition is false.
- It simplifies conditional expressions, especially for straightforward true/false checks.

Besides, `IF` operator has the following syntax:

```sql
IF(condition_expression, value_if_true, value_if_false);
```

# IF Example 🧪

In practice, `IF` is often used in the following use cases:

- *Data Categorization:*
    - Classifying data into categories based on certain conditions, such as labeling products as *"On Sale"* or *"Regular Price"*
- *Conditional Aggregation:*
    - Using the `IF` operator in aggregation functions to calculate sums or counts based on specific conditions.
- *Dynamic Outputs:*
    - Creating dynamic outputs in reports or dashboards by returning different values based on user-defined conditions.

For example, let’s create a simple comparison of two numbers:

```sql
SELECT IF(10 > 20, "TRUE", "FALSE");
```

Let’s classify apartments into one of two categories based on price:

- *"Comfort Class"*
- *"Economy Class"*

If the price is greater than or equal to 150, then the housing is classified as *"Comfort Class."*

```sql
SELECT
    id,
    price,
    IF(price >= 150, "*Comfort Class*", "*Economy Class*") AS category
FROM Rooms;
```

<aside>

💡 `IF` might be nested inside another `IF`

</aside>

```sql
SELECT
    id,
    price,
    IF(
        price >= 200, "Business-Class",
        IF(price >= 150, "*Comfort Class*", "*Economy Class*")
    ) AS category
FROM Rooms;
```

# IFNULL and NULLIF 🤷‍♂️

<aside>

💡
- `IFNULL` — returns a specified value if the expression is `NULL`
- If the expression is not `NULL`, it returns the expression's original value.

</aside>

<aside>

💡 `IFNULL` is useful for replacing `NULL` values with a default value

</aside>

Replacing `NULL` values can be helpful in preventing issues in calculations or reporting

<aside>

💡 `NULLIF` function compares two expressions and returns `NULL` if they are equal; otherwise, it returns the first expression. 

</aside>

This function is useful for avoiding division by zero or for handling conditional logic where you want to treat specific equal values as `NULL`.

# Examples 🧪

The functions have the following syntax:

```sql
IFNULL(expression, default_value)
NULLIF(expression1, expression2)
```

```sql
SELECT IFNULL(NULL, "Alternative SQL Academy") AS sql_trainer;
SELECT NULLIF("SQL Academy", "SQL Academy") AS sql_trainer;
```

# Important Notes ⚠️

- *Database Compatibility:*
    - The `IF` function is not available in all SQL dialects (like SQL Server or PostgreSQL). You may need to use the `CASE` statement instead.
- *Performance:*
    - Simple conditions should be preferred for performance reasons, as complex evaluations can slow down query execution.
- *Null Handling:*
    - Be cautious with `NULL` values in conditions, as they may affect the evaluation of the `IF` statement.