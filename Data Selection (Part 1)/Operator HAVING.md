# Operator HAVING

# Operator HAVING 🛒

After using `GROUP BY` clause to aggregate data, there are often scenarios where you want to further filter the resulting groups based on specific conditions. The `HAVING` clause is specifically designed for this purpose, allowing you to impose restrictions on the results of aggregate functions.

<aside>
📖

`HAVING` is used to filter the grouped data used in `GROUP BY`

</aside>

In order to apply those conditions on groups we use well-known functions like `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX` 

# HAVING Logic 🧩

Operator `HAVING` has the following syntax:

```sql
SELECT column1, agg_function(column2)
FROM table_name
GROUP BY column1
HAVING agg_function(column2) condition;
```

In *“Air BnB”* database let’s select only those that have on average price more than 100. In practice, it’s tempting to select the data using `WHERE` operator. However, this is incorrect. Again, we want to apply our conditions on groups and not columns!

<aside>
💡

`HAVING` filters groups, `WHERE` filters rows!

</aside>

So our final and correct query will look like this:

```sql
SELECT
		type AS apartment_type,
		AVG(price) AS avg_price
FROM apartment
GROUP BY type
HAVING AVG(price) > 100;
```

# HAVING Example 🧪

let's select the minimum price for each type of accommodation that has a Internet. Besides, let’s add an additional condition → total number of such apartments should be more than 5!

Here is the detailed explanation of how to get such result:

1. First, retrieve all data from the *apartment table*
2. Next, filter the records to include only apartments with a TV
3. Group the data by accommodation type
4. Filter the resulting groups based on the condition of having at least 5 apartments
5. Refer back to *SELECT* and include the necessary output

The final query will look like this:

```sql
SELECT
		type AS apartment_type,
		MIN(price) as min_price
FROM apartment
WHERE has_internet = True
GROUP BY type
HAVING COUNT(*) >= 5;
```

# **Important Notes ⚠️**

- *Post-Aggregation Filtering:* `HAVING` filters records after the aggregation has been performed. This means you can only use it to impose conditions on aggregate functions like `SUM()`, `COUNT()`, `AVG()`, …
- Important to know by heart *the order of SQL query execution*
- *Multiple Conditions:* Multiple conditions can be used in `HAVING`, combining them with logical operators like `AND` and `OR`