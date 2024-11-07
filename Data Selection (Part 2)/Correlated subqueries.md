# Correlated subqueries

# **Correlated Subqueries 🔗**

Unlike *regular subqueries*, which execute independently, a correlated subquery runs once for each row processed by the outer query. This relationship allows correlated subqueries to evaluate data on a row-by-row basis, making them useful for complex filtering and calculations.

<aside>
📖

**Correlated Subquery —** subquery that refers to columns from the outer query.

</aside>

# **Correlated Subquery Logic** 🧩

- A correlated subquery is evaluated row by row for the outer query, using values from the current row in the outer query.
- It typically appears in the `WHERE` clause but can also be used in `SELECT` or `HAVING` clauses.
- The *subquery* contains a reference to one or more columns from the outer query, creating a relationship between the two.

# Example 🧪

let’s find out who spent how much:

```sql
SELECT
		familymember.name,
		(
				SELECT SUM(payment.unit_price * payment.amount)
			  FROM payment
			  WHERE payment.family_member_id = familymember.id
	  ) AS total_spent
FROM familymember;
```

In this case, the correlated subquery references the `member_id` column from the main query.

# Advantages ⚡

- *Dynamic Filtering:*
    - They allow dynamic filtering based on outer query values, useful for customized, row-specific criteria.
- *Simplifies Nested Logic:*
    - Complex conditions involving multiple table comparisons can be simplified with correlated subqueries rather than lengthy joins or conditional logic.
- *Effective for Dependent Data:*
    - *Correlated subqueries* are well-suited for cases where rows in one table depend on specific conditions in another table.

# **Important Notes ⚠️**

- *Performance Impact:*
    - Since correlated subqueries run for each row in the outer query, they can be slower, especially with large data sets. Consider indexing columns used in the subquery to improve performance.
- *Limited to Certain Clauses:*
    - Correlated subqueries work best in `WHERE`, `SELECT`, and `HAVING` clauses but are less suited for some clauses like `FROM`.
- *Complex Readability:*
    - Because of the dependency on the outer query, correlated subqueries can make SQL statements harder to read and maintain. Clear comments or simpler alternative queries can help mitigate this.