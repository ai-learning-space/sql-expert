# Result Limiting | LIMIT 🚧

We may need to restrict a query output to control exactly how many rows we retrieve from a query, in such cases `LIMIT` is a nice operator.

<aside>

📖 `LIMIT` — is used to restrict the number of rows returned by a query.

</aside>

# LIMIT Logic 🧩

`LIMIT` operator usually has the following syntax:

```sql
SELECT column1, ...
FROM table_name
LIMIT number_of_rows;
```

For example, in “Air Travel” database let’s retrieve only first 5 flights ordered by *departure time:*

```sql
SELECT * 
FROM flight
ORDER BY departure_time
LIMIT 5;
```

💡 `LIMIT` clause is not implemented in all databases. For example, in MSSQL, the `TOP` clause is used to retrieve records from the start of the table, while the `OFFSET FETCH` construct is used for cases where you need to skip records from the beginning.

Besides, you can specify range of rows to retrieve:

```sql
-- retrieve rows 2 through 5
SELECT *
FROM flight
LIMIT 2, 5;
```