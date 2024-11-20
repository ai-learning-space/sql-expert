# UNION Operator 🔗

Sometimes we may want to unite the results from several queries. In such cases `UNION` operator can help us. 

<aside>

📖 **UNION** — operator in SQL is used to combine the results of two or more `SELECT` statements into a single result set.

</aside>

It allows you to retrieve data from multiple tables or queries and merge them together while eliminating duplicate rows.

# UNION Logic 🧩

- The `UNION` operator combines the results of two or more `SELECT` queries.
- Each `SELECT` statement must have the same number of columns in the result sets, and the columns must have compatible data types

<aside>

💡
  - `UNION` removes duplicate rows from the final result.
  - If you want to include duplicates, you can use `UNION ALL`

</aside>

Operator `UNION` has the following syntax:

```sql
SELECT column1, column2, ...
FROM table1
UNION [ALL]
SELECT column1, column2, ...
FROM table2;
```

It is important to distinguish between query unions and table joins, which are performed using the *JOIN* operator. Additionally, do not confuse query unions with subqueries, as subqueries operate on related tables.

<aside>

💡 The `UNION` operator is used to combine unrelated tables that share a similar structure.

</aside>

There are two other operators that behave similarly to `UNION`:

- `INTERSECT`:
    - Combines two `SELECT` queries but returns only the rows from the first `SELECT` that have matches in the second `SELECT`.
- `EXCEPT`:
    - Combines two `SELECT` queries but returns only the rows from the first `SELECT` that don’t  have matches in the second `SELECT`

# Example 🧪

Let’s retrieve the names of all products and the names of all family members (a somewhat arbitrary task), we can do so since the data types match.

```sql
SELECT DISTINCT Goods.good_name AS name FROM Goods
UNION
SELECT DISTINCT FamilyMembers.member_name AS name FROM FamilyMembers;
```

# When to Use UNION? 🤔

- *Aggregating Results:*
    - When you need to aggregate data from different tables or sources where the structure is similar.
- *Reporting:*
    - Useful in generating consolidated reports from multiple data sets.
- *Data Migration:*
    - When merging data from different periods or versions of a database.

# Important Notes ⚠️

- **Performance**:
    - Since `UNION` removes duplicates, it may take longer to execute compared to `UNION ALL`. If you know that duplicates are not an issue, prefer using `UNION ALL` for better performance.
- **Data Types**:
    - Ensure that the data types of the columns being combined are compatible. For example, you cannot union a string column with an integer column.
- **Column Names**:
    - The resulting column names in the final output will be taken from the first `SELECT` statement in the union.