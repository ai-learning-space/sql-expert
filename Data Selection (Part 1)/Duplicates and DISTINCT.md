# Duplicates and DISTINCT 👥

When working with databases, it's common to encounter duplicate values in columns or rows, especially when querying large datasets. These duplicates can lead to inaccurate reports, inflated metrics, and potentially misguided business decisions. Therefore, it's crucial to implement strategies for identifying, managing, and preventing duplicates to ensure the integrity of the data and the reliability of the insights drawn from it.

<aside>

📖 **Duplicates** — rows or values that appear more than once in a result set.

</aside>

Duplicates may appear because of the the following reasons:

- Multiple records in a table have the same value in one or more columns
- A query returns repeated rows due to joins or selections from a large dataset
- Lack of unique constraints in a database

<aside>

📖 `DISTINCT` — operator that removes duplicates and gets only unique values.

</aside>

```sql
-- DISTINCT syntax
SELECT DISTINCT column_names FROM table_name;
```

<aside>

💡 Behavior of `DISTINCT` is a bit different depending on number of selected columns.

</aside>

For example, in our *“Air Travel”* database let’s select only unique planes:

```sql
SELECT DISTINCT plane_name
FROM flight;
```

When we apply `DISTINCT` with multiple columns, SQL returns unique combinations of the values in those columns:

```sql
SELECT DISTINCT plane_name, departure_city
FROM flight;
```

# Important Notes ⚠️

- `DISTINCT` can impact query performance, especially on large datasets, because the database has to perform additional processing to identify and remove duplicates.
- When using `DISTINCT`, *NULL* values are treated as equal. If a column contains multiple *NULLs*, they will be displayed as a single *NULL* in the result set.
- When `DISTINCT` is applied on several columns, SQL returns only unique combinations of values for the selected columns.