# Subqueries 📦

Unfortunately, not all task in SQL can be done without using subqueries. For example, sometimes, you need to filter or calculate based on aggregate data that must be determined before the main query can use it. In such cases, using subqueries is must have.

<aside>

📖 **Subquery** — is a query nested inside another query.

</aside>

Subqueries are used to solve complex problems by breaking them into smaller, manageable parts that work together. Subqueries are often enclosed in parentheses and can appear in various parts of a query, such as the `SELECT`, `FROM`, `WHERE` or `HAVING` clauses.

# Subqueries Types 🎨

Subqueries have different types:

- *Single-Row Subquery*: returns only one row.
- *Multiple-Row Subquery:* returns multiple rows.
- *Multiple-Column Subquery:* returns multiple columns.
- *Correlated Subquery:* subquery that references columns from the outer query.

# Subquery Example 🧪

Let’s have a look at a single example by using *“Single-Row Subquery”* for *“Air BnB”* database:

```sql
SELECT *
FROM apartment
WHERE id = (
    SELECT id
    FROM apartment
    ORDER BY price DESC
    LIMIT 1
);
```

In this case, the query to obtain the most expensive room is executed as a *subquery* and the result set is then applied in the main query.

# Important Notes ⚠️

- *Subqueries* allow for *step-by-step* problem-solving in SQL.
- They are ideal for complex filters, aggregate comparisons and dependency on values calculated by other queries.
- *Subqueries* can slow down performance, so optimizing with indexes or breaking them into *joins* may help in large datasets.