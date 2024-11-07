# Window Functions

# Window Functions 🔍📊

*Window functions* allow you to perform calculations across a set of table rows that are somehow related to the current row.

<aside>
📖

**Window Function** — functions that perform calculations across a set of rows related to the current row without collapsing the results into a single output row. 

</aside>

Window functions allow you to analyze data across *"windows"* or *“specific ranges of rows”*, making them useful for tasks like *ranking*, *running totals* and *moving averages* within partitions of your data.

Below picture demonstrates visual difference between `GROUP BY` and `Window Function` 

![window-vs-aggregate.png](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/Advanced%20SQL/img/window-vs-aggregate.png)

# How Does it Work? **🤔**

You might wonder: *"What does 'window' mean?".* In a standard SQL query, all sets of rows are treated as a single continuous block of data, for which aggregate values are computed.

However, when *window functions* are applied, the query is segmented into groups of rows or *"windows"* and individual aggregate values are calculated for each of these segments. The window that we pass into a function can be:

- *Entire table*
- *Table Partition*
- *Range of Rows within a Table or Partition*

# Logic Visualization 📈

Let’s illustrate how a window function works by computing number of unique records for the “flight” table. First, we have to define what our windows will be. If you specify the entire table as the window, then the window will be the same for all rows and the same set of data will be fed to the *COUNT* function input and, accordingly, the result will be the same. 

![window-count.png](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/Advanced%20SQL/img/window-count.png)

Now, let’s check how the window function operates with different windows. For this purpose, we need to use *partitions*. 

<aside>
📖

**Partitioning** — divides the data into smaller subsets or *"partitions"* based on specified column values

</aside>

The window function then performs calculations within each partition independently. If we partition the above table by *“Air Company”*, we will get the following result:

![window-partition.png](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/Advanced%20SQL/img/window-partition.png)

Basically, partitioning splits the data into 2 groups (*KLM* and *Air France*), then window function is applied to each group independently and we get different result.

# Window Function Syntax **⚙️**

Window functions has the following syntax:

```sql
SELECT window_function(column_name)
OVER (
      [PARTITION BY columns_for_partitioning]
      [ORDER BY columns_for_sorting]
      [ROWS|RANGE row_range_definition]
)
```

- `window_function(column_name)` — is the window function used (e.g. `AVG(price)`)
- `OVER` — defines the window (group of rows) that will be passed to the window function.
    - If the `OVER` clause is left without parameters, the entire table will serve as the window.
    
    Now, to calculate the number of students in each class and display this information in a new column, we can use a window function:
    
- `PARTITION BY columns_for_partitioning` divides the result set into non-overlapping subsets, where each subset contains rows with the same values in one or more columns, forming partitions.
- `ORDER BY columns_for_sorting` sets the order of rows within the window, which is particularly important in ranking window functions.
- `ROWS|RANGE row_range_definition` defines ranges of rows. This parameter specifies how many rows to include before and after the current row in the window.

# Window Function Example 🧪

We defined some visual examples above, now it’s time to write the query. Let’s write a query to count number of unique planes per Air Company:

```sql
SELECT
		ac.name AS air_company_name
		COUNT(DISTINCT f.plane_name) OVER (PARTITION BY ac.name) AS unq_planes_count
FROM
		flight f
INNER JOIN aircompany ac ON ac.id = f.air_company_id;
```

- First we join a table `aircompany` to get names of air companies in the final output
- To get the count of unique planes, we use `COUNT(DISTINCT plane_name)`
- Since we want the result per air company, we apply `PARTITION BY air company name`

# Window Function Advantages ⚡

- *Flexible Data Analysis:*
    - Window functions support tasks like ranking, running totals, moving averages and lag/lead analysis, which are crucial in time series analysis, financial reporting and trend analysis.
- *Partitioned and Ordered Calculations:*
    - By defining partitions and ordering, you can apply calculations across specific groups (e.g., by department, month) and order the data within each group, giving highly customizable insights.
- *Efficient Performance:*
    - SQL window functions are often optimized for performance within databases, enabling faster execution for complex row-wise calculations compared to some traditional grouping and subquery techniques.
- *Enhanced Ranking and Row Comparison:*
    - With functions like `RANK()`, `ROW_NUMBER()`, `LAG()` and `LEAD()`, window functions allow easy row-to-row comparison, making them ideal for hierarchical ranking and trend analysis.