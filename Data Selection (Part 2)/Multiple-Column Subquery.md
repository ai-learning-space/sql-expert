# Multiple-Column Subquery 2️⃣📄

Unlike single-column subqueries, which return a single column, multiple-column subqueries can return two or more columns, each of which can be matched with columns in the main query.

<aside>

📖 **Multiple-Column Subquery** — subquery that returns more than one column of results.

</aside>

This is useful when you need to compare a combination of columns from one table against a combination of columns from another.

# Multiple-Column Subquery Logic 🧩

- A multiple-column subquery returns more than one column.
- In the main query, the combination of values from these columns can be compared to columns in the main query using operators like `IN` or specific comparisons between pairs of columns.
- It can be used in `WHERE` or `HAVING` clauses to filter rows based on multiple column values.

# Example 🧪

Let’s retrieve information about all reservations where the property price at the time of booking `booking.price` matches the current property price `apartment.price` :

```sql
SELECT * 
FROM apartment
WHERE (id, price) IN (SELECT id, price FROM apartment);
```

# Advantages ⚡

- *Composite Key Matching:*
    - They’re especially useful for composite key comparisons, allowing you to match rows across tables based on multiple conditions.
- *Dynamic Filtering:*
    - *Multiple-column subqueries* can dynamically retrieve and compare multi-column values without requiring multiple *single-column subqueries* or complex *joins*.
- *Enhanced Query Power:*
    - They expand the querying capability beyond what *single-column subqueries* offer, making it possible to handle more intricate data relationships.

# Important Notes ⚠️

- *Performance Overheads:*
    - As with any complex subquery, *multiple-column subqueries* may impact performance, especially when used with large data sets.
- *Readability:*
    - Using multiple fields in subqueries can make queries harder to read and maintain. Adding comments or breaking down complex conditions can help with clarity.
- *Supported Comparisons:*
    - Some database systems have limited support for *multiple-column comparisons,* so syntax and behavior might differ slightly depending on the system.