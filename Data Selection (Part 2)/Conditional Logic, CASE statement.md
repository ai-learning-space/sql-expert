# Conditional Logic, CASE statement

# CASE Operator ☝️

<aside>
📖

`CASE` — is a powerful tool for performing conditional logic within your queries.

</aside>

It enables you to create new columns based on specific conditions, making it easier to manipulate and analyze your data. The `CASE` operator can be used in `SELECT`, `UPDATE`, and `ORDER BY` statements.

# CASE Logic 🧩

Operator `CASE` has the following syntax:

- The `CASE` operator evaluates conditions in the order they are written and returns the first true condition's result.
- It can return different values based on different conditions, making it useful for categorizing or transforming data.

```sql
SELECT
		column1,
		CASE column2
				WHEN value1 THEN result1
				WHEN value2 THEN result2
				...
				ELSE default_result
		END AS new_column
FROM table_name;
```

# Example 🧪

Let’s assig a age category to a person:

```sql
SELECT
		name,
		status,
CASE
	  WHEN TIMESTAMPDIFF(YEAR, birthday, NOW()) >= 18 THEN "Mature"
	  ELSE "Teenager"
END AS status
FROM familymember;
```

Let's examine the `CASE` operator with an example of determining a student's education level.

```sql
SELECT
		name,
		CASE
			WHEN SUBSTRING(name, 1, INSTR(name, ' ')) IN (10, 11) THEN "Старшая школа"
			WHEN SUBSTRING(name, 1, INSTR(name, ' ')) IN (5, 6, 7, 8, 9) THEN "Средняя школа"
		ELSE "Начальная школа"
		END AS stage
FROM Class
```

# Important Notes **⚠️**

- *Performance:*
    - While the `CASE` operator is efficient, overly complex conditions can impact query performance. It's advisable to keep conditions straightforward.
- *Null Handling:*
    - Be aware of how `NULL` values are treated in conditions, as they can affect the outcome of the `CASE` evaluation.
- *Readability:*
    - Use clear and concise `CASE` expressions for better readability, especially in complex queries.