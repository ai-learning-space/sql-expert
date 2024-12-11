# Operator WHERE 🔍

We often need not only to query data but also to filter it to retrieve only the relevant information. This is when `WHERE` operator shines and makes our life easier. The `WHERE` clause is one of the most commonly used parts of an SQL query. It allows you to filter records from a table, so you can retrieve only the rows that meet specific conditions. This is important when you want to narrow down your data to retrieve only relevant information.

<aside>

📖 `WHERE` — is an operator in SQL used for data filtering.

</aside>

Operator `WHERE` has the following syntax:

```sql
SELECT ...
FROM table_name
WHERE condition;
```

For example, let’s find out flights from *Paris on Boeing 737 plane using “Air Travel"* database:

```sql
SELECT * 
FROM flight
WHERE plane_name = "Boeing 737" AND departure_city = "Paris";
```

In the query above we used two comparison operations that were combined by using `AND` . The `WHERE` clause can work with *Numbers*, *Text*, *Dates* and *Boolean* logic, making it very flexible. You can even use it with operators like `>`, `<`, `BETWEEN` and `LIKE` for more refined filtering. This makes `WHERE` fundamental for complex queries and efficient data handling.

# Comparison Operators ⚖️

Comparison operators are used within the `WHERE` clause to compare values in columns against specific criteria, allowing you to filter records based on conditions. These operators are essential for defining exact matches, range checks, or complex filtering. When the expressions are compared, they result in:

- `TRUE` → equivalent to 1
- `FALSE` → equivalent to 0
- `NULL` → empty, nothing

| **Operator** | **Symbol** | **Description** |
| --- | --- | --- |
| *Equality* | `=` | If both values are equal, the result will be 1; otherwise, it will be 0. |
| *Equivalence* | `<=>` | Similar to the equality operator, but returns 1 when comparing *NULL* with *NULL* and 0 when comparing any value with *NULL*. |
| *Inequality* | `<>` or `!=` | If both values are not equal, the result will be 1; otherwise, it will be 0. |
| *Less* | `<` | If one value is less than another, the result will be 1; otherwise, it will be 0. |
| *Less or Equal* | `<=` | If one value is less than or equal to another, the result will be 1; otherwise, it will be 0. |
| *Greater* | `>` | If one value is greater than another, the result will be 1; otherwise, it will be 0. |
| *Greater or Equal* | `>=` | If one value is greater than or equal to another, the result will be 1; otherwise, it will be 0. |

<aside>

💡 Comparison of any values with `NULL` returns `NULL` , except for equivalence operator.

</aside>

For better understanding, you can play around with the code below:

```sql
SELECT
    2 = 1,
    'a' = 'a',
    NULL <=> NULL,
    2 <> 2,
    3 < 4,
    10 <= 10,
    7 > 1,
    8 >= 10;
```

# Logical Operators 🧠

It’s nice if we could combine several conditions together and this is possible in SQL by using *logical operator*. *Logical operators* are used to combine multiple conditions in a `WHERE` clause, enabling more complex filtering of records based on specific criteria. These operators help refine queries by allowing you to specify relationships between different conditions.

<aside>

💡 *Logical Operators* are essential for connecting comparison operators.

</aside>

The table below describes the main logical operators:

| **Operator** | **Description** |
| --- | --- |
| `NOT` | Negates the value of the comparison operator. |
| `OR` | Returns true if at least one of the expressions is true. |
| `AND` | Returns true only if both expressions are true. |
| `XOR` | Returns true if exactly one of the arguments is true. |

For example, let's select all flights that were made on a “*Airbus A380*” airplane, ensuring that the departure city is not *Berlin*:

```sql
SELECT *
FROM Trip
WHERE plane = 'Airbus A380' AND NOT town_from = 'Berlin';
```