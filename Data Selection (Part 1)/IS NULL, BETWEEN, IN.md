# IS NULL, BETWEEN, IN

# IS NULL, BETWEEN, IN

Effectively managing and querying data often involves the use of specific operators that help refine and filter results. Among these `IS NULL`, `BETWEEN` and `IN` operators play crucial roles in identifying missing values, specifying ranges and checking for multiple values within a dataset.

Understanding how to utilize these operators can greatly enhance your ability to extract meaningful insights from databases, making your queries more efficient and precise. In this section, we will explore each operator in detail, providing examples and use cases to illustrate their importance in SQL queries.

# IS NULL **🤷‍♂️**

The `IS NULL` operator is used to check for *missing or NULL values* in a column.

<aside>
💡

`NULL` represents the absence of a value — it means that the field is empty or unknown.

</aside>

For example, in database *“Air Travel”* let’s select passengers that don’t have name:

```sql
SELECT * 
FROM passenger
WHERE name IS NULL;

-- to use negation, meaning if we want to find all records where the field is not NULL
SELECT * 
FROM passenger
WHERE name IS NOT NULL;
```

# BETWEEN ↔️

Sometimes we need to select only those records where values are between specific range of values.

<aside>
💡

`BETWEEN` is used to filter the result set within a specified range including start and end

</aside>

In *“Air BnB”* database let’s select only those bookings where price between 100 and 250dollars:

```sql
SELECT *
FROM booking
WHERE price BETWEEN 100 AND 250;
```

- The values can be *numbers*, *dates* or even *text*, depending on how the column is stored.
- The range is *inclusive*, meaning it includes both `100` and `250`

# IN 👉

If we are interested in only specific values, we can specify them by using `IN` 

<aside>
💡

`IN` is used to specify multiple possible values for a column

</aside>

It helps you filter out records that match any value in a given list.

```sql
SELECT *
FROM apartment
WHERE type IN ('Private room', 'Entire home/apt');
```

- You can list as many values as needed inside the parentheses.
- `IN` is useful when you want to match several specific values without using multiple `OR`