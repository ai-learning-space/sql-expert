# Result Ordering | ORDER BY ➡️

When executing a `SELECT` query, the rows are returned in an *undefined order* by default. This means that unless you explicitly specify an ordering using the `ORDER BY` clause, the *database* may return the results in any order, which can vary between executions and may not be predictable. 

As a result, relying on this default behavior can lead to inconsistent results, especially when working with large datasets or when the underlying data is modified frequently. To ensure that your results are presented in a specific sequence, it's essential to use `ORDER BY`

<aside>

📖 `ORDER BY` — is used for sorting of the final result set based on one or more columns

</aside>

# ORDER BY Logic 🧩

`ORDER BY` has the following syntax:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE ...
ORDER BY column_1 [ASC | DESC], column_2 [ASC | DESC]
```

<aside>

💡 One or more columns can be used in `ORDER BY`

</aside>

You can specify whether the sorting should be in ***ascending*** or ***descending*** order:

- `ASC` → ascending order (default)
- `DESC` → descending order

In *“Air Travel”* database, let’s select names of passengers in *alphabetical order*:

```sql
SELECT name
FROM passenger
ORDER BY name ASC;
```

<aside>

💡 `ASC` is used by default and an be omitted, only `DESC` requires explicit definition

</aside>

Below table demonstrates sorting of different data types:

| **Data Type**  | **Ascending**                                   | **Descending**                                  |
|-----------------|------------------------------------------------|------------------------------------------------|
| *String*        | Lexicographical order from `"A"` to `"Z"`. Records starting with `"a"` come first, followed by `"b"`, and so on. | Lexicographical order from `"Z"` to `"A"`. Records starting with `"z"`, `"y"`, and so forth come first. |
| *Numeric*       | From smaller to larger                        | From larger to smaller                         |
| *Date/Time*     | From earlier dates/times to later ones. For example, `01.01.2024` comes before `01.02.2024`. | From later dates/times to earlier ones. For example, `01.02.2024` comes before `01.01.2024`. |
| *Boolean*       | *False* comes before *True*                   | *True* comes before *False*                   |


# Multiple Columns Sorting ✨

To sort results by two or more columns, we simply need to enumerate them. For example, let’s retrieve information about flights sorted by the departure city in *ascending* order and the arrival city in *descending* order from `flight` table:

```sql
SELECT DISTINCT
    departure_city,
    arrival_city
FROM flight
ORDER BY departure_city ASC, arrival_city DESC;
```

# Important Notes ⚠️

- When using multiple columns in `ORDER BY`, SQL will first sort by the first column, and if there are ties, it will move to the next column.
- The result set order is important in use cases like *ranking*, *pagination* and displaying results in a particular sequence.