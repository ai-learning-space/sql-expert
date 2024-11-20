# Window Functions Types 🔍📊

We explored how *window functions* work and introduced the concept of a *data window* that is passed to a *window function*. Now it's time to examine the different types of window functions.

Window functions can be categorized into three groups:

- *Aggregate Window Functions* 📊
- *Ranking Window Functions* 🥇🥈🥉
- *Offset Window Functions* ⬅️➡️

![window-function-types.png](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/Advanced%20SQL/img/window-function-types.png)

# Aggregate Window Functions 📊

<aside>

📖**Aggregate Window Functions** —  perform arithmetic calculations on a dataset and return a single summary value

</aside>

For example: 

- `SUM` **→** calculates the total *sum of values*
- `COUNT` **→** counts the total *number of records* in a column
- `AVG` **→** computes the *average value*
- `MAX` **→** finds the biggest value
- `MIN` **→** determines the lowest value

Let’s practice the above functions on “Apartments” table:

```sql
SELECT
    type AS apartment_type,
    price AS apartment_price,
    SUM(price) OVER(PARTITION BY type) AS 'sum_price',
    COUNT(price) OVER(PARTITION BY type) AS 'count_price',
    AVG(price) OVER(PARTITION BY type) AS 'mean_price',
    MAX(price) OVER(PARTITION BY type) AS 'max_price',
    MIN(price) OVER(PARTITION BY type) AS 'min_price'
FROM apartment;
```

# Ranking Window Functions 🥇🥈🥉

Ranking window functions assign a rank to each value within a window. In ranking functions, the keyword `OVER` requires the specification of an `ORDER BY` clause, which determines the sorting order for the ranking.

- `ROW_NUMBER` **→** returns the row number, used for numbering
- `RANK` **→** returns the rank of each row
- `DENSE_RANK` **→** similar to *RANK*, but it assigns ranks without skipping any values for tied rows

```sql
SELECT
    type AS apartment_type,
    price AS apartment_price,
    ROW_NUMBER() OVER(PARTITION BY type ORDER BY price) AS 'row_number',
    RANK() OVER(PARTITION BY type ORDER BY price) AS 'rank',
    DENSE_RANK() OVER(PARTITION BY type ORDER BY price) AS 'dense_rank'
FROM apartment;
```

For example, the function *RANK* works in the following way:

1. *Sorting*: first, rows are sorted based on one or more specified columns in the `ORDER BY` clause within the `OVER` construct.
2. *Assigning Ranks:* each unique row or group of rows with identical sorting values is assigned a *rank*, starting from 1.
3. *Tied Values*: if multiple rows have the same sorting values, they receive the same rank. For example, if two rows are tied for second place, both will receive a *rank* of 2.
4. *Skipping Ranks:* after a group of rows with the same rank, the next rank increases by the number of rows in that group. For example, if two rows have a rank of 2, the next row will receive a rank of 4, not 3.
5. *Continuing the Sorting:* this process continues until all rows in the result set are assigned ranks.

# Offset Window Functions ⬅️➡️

*Offset window functions* allow you to navigate and access different rows within a window relative to the current row, as well as reference values at the beginning or end of the window.

- `LAG` **→** accesses data from previous rows in the window. It has three arguments: the column whose value you want to return, the number of rows to offset (default is 1), and a value to return if the offset results in a *NULL*.
- `LEAD` **→** accesses data from subsequent rows, similar to *LAG*, and also has three arguments.
- `FIRST_VALUE` **→** returns the first value in the window. It takes a column as an argument to specify which value to return.
- `LAST_VALUE` **→** returns the last value in the window, taking a column as an argument.

```sql
SELECT
    type AS apartment_type,
    price AS apartment_price,
    LAG(price) OVER(PARTITION BY type ORDER BY price) AS 'lag',
    LAG(price, 2) OVER(PARTITION BY type ORDER BY price) AS 'lag_2',
    LEAD(price) OVER(PARTITION BY type ORDER BY price) AS 'lead',
    FIRST_VALUE(price) OVER(PARTITION BY type ORDER BY price) AS 'first_value',
    LAST_VALUE(price) OVER(PARTITION BY type ORDER BY price) AS 'last_value'
FROM apartment;
```