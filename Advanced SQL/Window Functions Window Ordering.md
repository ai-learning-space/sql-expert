# Window Functions  | Window Ordering

# **Ordering Within a Window 📏**

In previous articles, we explored window functions and partitioning in SQL. Now, let's move on to another important aspect of window functions — *sorting within a window*.

# **Why Ordering in a Window Important? 🤔**

Sorting in SQL window functions is key to advanced data analysis. It allows to order data within a specific group or window, providing more accurate and targeted aggregate calculations. This is particularly useful when dealing with time series data, where the order of events matters or when ranking data within groups.

# Example 🧪

Suppose we need to analyze booking data for accommodations to determine how the total amount spent on rentals has changed over time for each user. To achieve the desired result, we first need to partition the data by each user so that the window function operates independently for each user. To calculate the total, we can use the window function `SUM`.

```sql
SELECT
		user_id,
		checkin_date,
    total AS reservation_price,
    SUM(total) OVER (
		    PARTITION BY user_id
    ) AS total_expenses
FROM booking;
```

As a result of the executed query, the `total_expenses` column displays the total amount spent, broken down by user. However, this is not exactly what we want: the data in the table is not ordered by date and we cannot see how the total expenses grew over time; we only see the final expenses.

To achieve the desired result, we need to add ordering by the reservation start date to the query:

```sql
SELECT
		user_id,
    checkin_date,
    total AS reservation_price,
    SUM(total) OVER (
		    PARTITION BY user_id
        ORDER BY checkin_date
    ) AS cumulative_total
FROM booking;
```

Now we have achieved what we wanted. But what changed after adding `ORDER BY checkin_date`?

- The data within the partition is now sorted by the reservation check-in date.
- The method for calculating the total amount spent has changed: the sum within the partition accumulates instead of being displayed as a final value. This is related to a particular feature of using sorting without explicitly specifying `ROWS|RANGE` in the `OVER` clause. Let's elaborate on this.

# Ordering Without Specifying Window Bounds 🚧

As we recall, the full syntax of the window function looks like this:

```sql
SELECT window_function(table_column)
OVER (
      [PARTITION BY partition_columns]
      [ORDER BY sort_columns]
      [ROWS|RANGE row_range_definition]
)
```

In addition to the `PARTITION BY` and `ORDER BY` clauses, there is an optional `ROWS|RANGE` clause. We will discuss this in detail in the next article, but for now, it’s important to understand its purpose. It allows you to specify the window bounds relative to the current row that will be used for calculations in the window function.

Thus, you can specify that when calculating values for the current row, the window function should include only N records before the current row and N after it, rather than all records within the current partition. When using `ORDER BY`, if nothing is specified in the `ROWS|RANGE` clause, the window function automatically applies the rule `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`. This means that the window will start from the first row and end at the current row.

In other words, the values for the `cumulative_total` column will be calculated as follows: