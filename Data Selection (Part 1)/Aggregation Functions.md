# Aggregation Functions 🗃️

*Aggregation functions* are powerful tools in SQL that enable users to perform calculations on multiple rows of data, returning a single value for each group of records. They play a crucial role in data analysis, allowing users to summarize and interpret large datasets effectively. 

<aside>

📖 **Aggregation Function** — is a function used to perform a calculation on a set of values and returns a single value.

</aside>

*Aggregation functions* are commonly used in combination with `GROUP BY` to perform aggregation. However, they can be also applied without `GROUP BY`. Let’s quickly look at the syntax:

```sql
SELECT agg_function(column_name)
FROM table_name
GROUP BY column_name;
```

The table below describes most common aggregation functions used in SQL:

| **Function** | **Description** |
| --- | --- |
| `SUM()` | Returns the sum of values |
| `AVG()` | Returns the average value |
| `COUNT()` | Returns the count of records |
| `MIN()` | Returns the minimum value |
| `MAX()` | Returns the maximum value |
| `COUNT(*)` | Returns the count of records (including NULL) |

<aside>

💡 Aggregation functions exclude `NULL` values except for `COUNT(*)`

</aside>

# Examples 🧪

in “Air Travel” database, let’s find out how may flights has been done on “Boeing 777”:

```sql
SELECT plane_name, COUNT(*) AS flights_count
FROM flight
WHERE plane_name = 'Boeing 777'
GROUP BY plane_name;
```

In “Air BnB” database, let’s find out the price of the most expensive booking:

```sql
SELECT MAX(price)
FROM booking;
```

In “Air BnB” database, find out the most expensive price for each apartment type:

```sql
SELECT
    type AS apartment_type,
    MAX(price) AS max_price
FROM
    apartment
GROUP BY
    type
```

# Importance of Aggregation Functions 📌

- **Data Summary**:
    - They provide a way to summarize large datasets, allowing for easier interpretation and reporting.
- **Trend Analysis**:
    - By applying aggregation functions, users can identify trends over time, such as average sales per month or total customer counts.
- **Decision Making**:
    - Aggregated data supports business intelligence and decision-making processes by providing essential insights.