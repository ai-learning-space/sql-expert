# Multi-Table Queries, JOINs 🤝

In SQL, we usually deal with many tables, and it’s unlikely in real life that you’ll need to work with just a single table. Most databases are structured with multiple tables that store related information separately to improve organization, reduce redundancy and maintain data integrity. To analyze data or generate reports, we often need to combine data from these tables, which is where SQL `JOIN` operations come in.

Using *JOINs*, we can link tables together based on related columns. For instance, you may have noticed that in tables we have *IDs* that refer to *IDs* in another table → *Foreign Keys*. By using these keys you can put together relevant data across all tables in one query.

# JOIN Logic 🧩

To link several tables together, we need to use the following syntax of *JOIN*. For example, for “Air Travel” database let’s list the following info: *departure city*, *arrival city*, *plane name* and *air company name*. We may notice that a*ir company name* is only available in another table and to retrieve that data we use *JOIN*:

```sql
SELECT
    f.plane_name,
    f.departure_city,
    f.arrival_city,
    ac.name AS air_company_name
FROM flight f
INNER JOIN aircompany ac ON f.air_company_id = ac.id
```

In the above example we used `INNER JOIN` (there are many different *JOINs* in SQL) and operator `ON` to define on what columns we merge/link the data. General syntax of *JOINs* may look like this:

```sql
SELECT column1, ...
FROM table_1
INNER | LEFT | RIGHT | FULL JOIN table_2 ON join_condition
INNER | LEFT | RIGHT | FULL JOIN JOIN table_n ON join_condition
```

<aside>

💡 Many different *JOINs* can be used in a single query.

</aside>

# JOIN Types 🎨

There are many types of different *JOINs:*

| **Join Type** | **Description** | **Result** |
| --- | --- | --- |
| `INNER JOIN`  | Returns rows that have matching values in both tables. | Only rows where there is a match in both tables are returned. Rows with no match in either table are excluded. |
| `LEFT JOIN` | Returns all rows from the left table and the matching rows from the right table. | All rows from the left table are included. If there is no match in the right table, `NULL` values are returned for columns from the right table. |
| `RIGHT JOIN` | Returns all rows from the right table and the matching rows from the left table. | All rows from the right table are included. If there is no match in the left table, `NULL` values are returned for columns from the left table. |
| `FULL JOIN` | Returns all rows when there is a match in either table. | All rows from both tables are included. If there is no match, `NULL` values are returned for columns from the other table. |
| `CROSS JOIN` | Returns the Cartesian product of both tables. | Each row from the left table is combined with each row from the right table. If the left table has 3 rows and the right table has 4 rows, the result will have 12 rows. |
| `SELF JOIN` | A *JOIN* where a table is joined with itself. | Useful for hierarchical or recursive data structures. It matches rows from the same table based on some relationship (usually with an alias to distinguish the tables). |
| `NATURAL JOIN` | Automatically joins tables based on columns with the same name in both tables. | The `JOIN` is performed on columns with the same names in both tables without specifying `ON`. The common columns must have identical data types. |

In some cases, you might want to select all columns from only a specific table. For example, given a join between `flight` and `aircompany`, you may want to retrieve only the columns from `flight` 

How can this be done? It's simple! Just prepend the table name before the `*` symbol:

```sql
SELECT
    f.*, ac.*
FROM flight f
INNER JOIN aircompany ac ON f.air_company_id = ac.id
```