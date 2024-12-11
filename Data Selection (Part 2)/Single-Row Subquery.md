# Single-Row Subquery 1️⃣📄

In this section we will cover a subquery that returns a single row and a single column. 

<aside>

📖 **Scalar Subquery** — subquery that returns single row and a single column.

</aside>

It’s helpful when you need to retrieve a calculated or aggregated value from one part of a database and use it in another part, without needing to join tables or use multiple queries. Scalar subqueries can be used in various parts of the main SQL query, but they are most commonly used in filtering conditions with comparison operators: `=, <>, >, <`

# Query Example 🧪

Let’s have a look at examples of using scalar subquery in different places of SQL query:

*SELECT Clause:*

```sql
-- add "mean booking price"
SELECT *, (SELECT AVG(price) FROM booking) AS avg_price FROM booking;
```

*FROM Clause:*

```sql
-- add new column without JOINs -> add mean price of apartments
SELECT
    apt.*,
    apt_avg.*
FROM
    apartment apt,
    (
        SELECT AVG(price) AS avg_apartment_price
        FROM apartment
    ) AS apt_avg;
```

*WHERE Clause:*

```sql
-- select only those bookings that are less than "mean booking price"
SELECT *, (SELECT AVG(price) FROM booking) AS avg_price
FROM booking
WHERE price <= (SELECT AVG(price) FROM booking);
```

*HAVING Clause:*

```sql
-- select only those apartments that are more expensive than "mean apartment price"
SELECT type, AVG(price) AS avg_price
FROM apartment
GROUP BY type
HAVING AVG(price) <= (SELECT AVG(price) FROM apartment);
```

<aside>

💡 Validate what result the subquery returns and what operators allowed with the result set

</aside>

# Advantages ⚡

- ***Improved Readability:***
    - Scalar subqueries can make complex queries more readable by encapsulating calculations or values you need repeatedly.
- ***Modular Calculations:***
    - They allow you to handle calculations separately within the query.
- ***Powerful Aggregation Options:***
    - Useful in scenarios where simple joins wouldn’t provide the aggregated data needed.

# Important Notes⚠️

- ***Performance Impact:***
    - While convenient, scalar subqueries can slow down query execution, especially when used repeatedly in clauses like `SELECT` or `WHERE`.
- ***Usage Limits:***
    - Scalar subqueries should ideally return only one row. If they accidentally return more, SQL will produce an error. Use `LIMIT` or other filters if you’re not certain it will always be a single value.