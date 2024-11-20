# INNER JOIN 🎯

This *JOIN* is used to retrieve the rows that are matched in both tables

<aside>

💡 `INNER JOIN` is used to combine rows from two or more tables that are matched

</aside>

It’s commonly used when you want to see only the data that exists in both sources. Let’s closer look at the logic:

- The `JOIN` compares the columns specified in the `ON` clause.
- Only rows where the values in the related columns are equal in both tables will be included in the result set.
- If there is no match between the rows, they are excluded from the result.

For example, in *“Air Travel”* database when we merge *“aircompany”* and *“flight”, INNER JOIN* works in the following way:

![inner-join.png](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/Data%20Selection%20(Part%202)/img/inner-join.png)

The query will have the following structure:

```sql
SELECT *
FROM flight f
INNER JOIN aircompany ac ON f.air_company_id = ac.id
```

# INNER JOIN and WHERE 🔗

You can implement `INNER JOIN` using the `WHERE` clause by specifying the condition that would typically be defined in the `ON` clause of an `INNER JOIN`. This approach works because an `INNER JOIN` only includes rows where the condition between the tables is met, which can also be achieved by filtering with `WHERE`.

<aside>

💡 `INNER JOIN` can be implemented by using `WHERE`

</aside>

However, using explicit `JOIN` syntax is generally preferred because:

- It improves readability, making it clear you’re joining tables.
- It’s more consistent with SQL best practices, especially for complex joins or when mixing different join types.