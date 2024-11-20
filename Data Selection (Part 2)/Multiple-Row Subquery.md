# Multiple-Row Subquery 2️⃣📄

Subquery may not always return a single value, as opposed to a scalar subquery. *Multiple-row subqueries* are typically used when we want to compare a value to a list of possible matches or fetch a subset of data that can be compared with multiple values in the main query.

<aside>

📖 **Multiple-Row Subquery** is a subquery that returns more than one row of results.

</aside>

Since the subquery can return multiple values, it must be used with specific operators that can handle multiple results, such as `IN`, `ANY` or `ALL`. Let’s dive into these operators one by one.

# ALL Operator 👐

<aside>

📖 `ALL` operator is used to compare a value to every value in a list or the result of a subquery

</aside>

It ensures that a condition is *true* for *all values* returned by the subquery. The `ALL` operator works with comparison operators like `=, >, <, >=, <=, <>` 

### ALL Logic 🧩

- The comparison condition is applied to *every value* in the result set of the subquery.
- The main query only returns rows if the condition is *true* for *all* the values produced by the subquery.

### Example 🧪

Let’s check if all apartments are priced lower than 200:

```sql
SELECT 200 > ALL(SELECT price FROM apartment);
```

# ANY Operator 🔄

<aside>

📖 `ANY` operator compares a value to any value in a list or the result of a subquery

</aside>

It is used with comparison operators such as `=, >, <, >=, <=, <>` . The `ANY` operator returns *true* if at least one of the values in the list or subquery satisfies the condition.

### ANY Logic 🧩

- When you use `ANY`, the comparison condition is evaluated against each value returned by the subquery.
- If at least one comparison is `TRUE`, the overall condition is `TRUE`.

### Example 🧪

Let’s find users who own at least one property valued over 150:

```sql
SELECT *
FROM client
WHERE id = ANY (
    SELECT DISTINCT owner_id
    FROM apartment
    WHERE price >= 150
);
```

# IN Operator 👉

<aside>

📖 `IN` operator is used to check whether a value matches any value within a list or a subquery

</aside>

It simplifies multiple `OR` conditions and is commonly used for filtering rows based on a set of values.

### IN Logic 🧩

- The `IN` operator allows you to compare a value against a list of values. If the value matches any of the values in the list, the condition evaluates to `TRUE`.
- It can be used with both static value lists and subqueries that return a set of values.

### Example 🧪

Let’s find all information about owners of properties priced above 150:

```sql
SELECT *
FROM apartment
WHERE id IN (
    SELECT DISTINCT owner_id
    FROM apartment
    WHERE price >= 150
);
```

# Advantages ⚡

- *Flexible Comparison:*
    - Multiple-row subqueries allow for dynamic comparisons against a set of values, making it easy to filter data based on complex conditions.
- *Dynamic Filtering:*
    - With operators like `IN` or `EXISTS`, they can filter data dynamically, adapting to changes in related tables without modifying the main query.
- *Support for Correlated Logic:*
    - Using correlated subqueries with `EXISTS`, you can achieve row-by-row comparisons that are difficult to replicate with simple joins.