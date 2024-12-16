# Data Grouping | GROUP BY 👨‍👩‍👧‍👦

In the world of databases, analyzing large datasets often requires more than just retrieving raw data, it demands a method to organize and summarize that information effectively. This is where the `GROUP BY` clause in SQL comes into play.

By allowing users to group rows sharing common values in specified columns, `GROUP BY` makes it possible to perform aggregate functions like `SUM`, `COUNT` and `AVG` on these groups. This powerful feature not only simplifies complex queries but also enhances data analysis, enabling better insights and decision-making. 

<aside>

📖 `GROUP BY` is used to group rows that have the same values in specified columns and then perform aggregate functions like `COUNT`, `SUM`, `AVG`, `MAX`, `MIN` on those groups.

</aside>

Let's execute the query:

```sql
SELECT id, plane_name, departure_city, arrival_city
FROM flight;
```

Good, we obtained information about each flight. But what if we want information not about each individual record, but about the groups they form?

For example, these groups could be defined by:

- *Departure City* → *“How many flights we have from City A?”*
- *Plane Name* → *“How many flights we have per plane?”*
- …

These groups include different records in the table and, consequently, have various characteristics that can be very useful to us. Such useful information about the groups could include:

- *Total number of flights per plane*
- *Air company with the biggest number of flights*
- …

To answer all these and many other questions, we use the `GROUP BY` operator.

# GROUP BY Logic 🧩

All we have to do is just to define `GROUP BY` keyword and *columns* on which we would like to create those groups for following aggregation operations.

```sql
SELECT agg_function(column_name)
FROM table_name
GROUP BY column_a, column_b;
```

Once `GROUP BY` is applied we don’t work with single *records* anymore, we work with *groups*! As a result, we cannot simply select any field from a *record* as we could before. This is because each *group* may contain multiple *records*, each of which may have different values in those fields.

For example, let’s find out how many unique flights has each air company in “Air Flights” database:

```sql
SELECT plane_name, COUNT(DISTINCT plane)
FROM flight
GROUP BY plane_name;
```

Above query can be visualized in the picture below:

![data-grouping.png](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/Data%20Selection%20(Part%201)/img/data-grouping.png)

- First we obtain groups defined in `GROUP BY`
- Aggregation function is applied to the groups → `COUNT(DISTINCT plane)`

<aside>

💡 `GROUP BY` treats `NULL` values equal. If filed contains `NULL` , all rows will be placed in the same group.

</aside>

let’s find out how many flights we have per plane:

```sql
SELECT plane_name, COUNT(*) AS flights_count
FROM flight
GROUP BY plane_name;
```

# Grouping by Two or More Fields ➕

When grouping by two or more fields, the principle remains the same. However, the resulting groups are further divided into smaller groups based on the second grouping field.

```sql
SELECT plane_name, departure_city, COUNT(*) AS flights_count
FROM flight
GROUP BY plane_name, departure_city;
```

# Why Using GROUP BY? 🤔

- ***Data Summarization:***
    - Easily summarize and aggregate large datasets to gain insights.
- ***Enhanced Analysis:***
    - Enables more complex analysis by allowing calculations based on specific groups within your data.
- ***Cleaner Data Presentation:***
    - Helps in presenting data in a more organized and readable format, focusing on key metrics.