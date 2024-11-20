# Functions in SQL 🔢

In real-life SQL queries complexity often arises because they are used to handle multiple layers of aggregation, data transformations and formatting tasks within a single query. In such cases, SQL functions reduce processing time and keep SQL queries readable and maintainable.

<aside>

📖 **SQL Functions** — built-in operations allowing to perform calculations, manipulate data, and retrieve specific information directly within your SQL queries.

</aside>

They help streamline data processing and enhance query efficiency by eliminating the need for additional calculations. SQL provides a wide range of *built-in functions* that help performing operations on data. These functions are categorized into several types, depending on the kind of operations they perform. For example, if we want to lower case a string, we may use `LOWER` function:

```sql
SELECT LOWER("Hi, This is Lower Case Function");
```

# What is a Built-in Function? 🤔

<aside>

📖 **Built-in Function —** pre-defined function provided by the database system that performs a specific task or operation. These functions are integrated into the SQL language and are readily available for use without needing to write custom code.

</aside>

*Built-in functions* take one or more *arguments/inputs*, process them and return a result. For example, you might use a *built-in function* to:

- Calculate the average of a numeric column → `AVG()`
- Convert text to uppercase → `UPPER()`
- Get the current date and time → `NOW()`

```sql
SELECT
    NOW() AS curent_datetime,
    LENGHT("Hi. I'm learning SQL") AS str_length;
```

<aside>

💡 Functions can be applied not only to literals but also to values retrieved from a table. 
In this case, the function processes each row individually.

</aside>

For example, let’s check out `client` table and do the following tasks:

1. Lowercase client name
2. Take only 5 first letters (assume we need it)

```sql
SELECT
    LEFT(LOWER(name), 5) AS client_name_low_first_5
FROM
    client;
```

# Type of Built-in Functions 🎨

SQL functions can be broadly categorized into several types. Depending on your task and having the below table at hand you can quickly decide what you need:

| **Type**                | **Functions**                                     | **Example**                                                                                          |
|--------------------------|--------------------------------------------------|------------------------------------------------------------------------------------------------------|
| *Aggregate Functions*    | `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`    | `SUM(sales_amount)`<br>`MIN(price)`<br>`AVG(sales)`                                                 |
| *String Functions*       | `UPPER()`, `LOWER()`, `SUBSTRING()`, `LENGTH()`, `CONCAT()` | `LOWER(name)`<br>`CONCAT(first_name, ' ', last_name)`<br>`SUBSTRING(name, 1, 3)`                  |
| *Date and Time Functions*| `NOW()`, `DATEADD()`, `DATEDIFF()`, `YEAR()`, `MONTH()`, `DAY()` | `DATEADD(DAY, 7, order_date)`<br>`DATEDIFF(DAY, start_date, end_date)`<br>`DATEPART(QUARTER, sale_date)` |
| *Mathematical Functions* | `ROUND()`, `ABS()`, `POWER()`, `MOD()`           | `POWER(2, 3)` → `8`<br>`MOD(10, 3)` → `1`<br>`ABS(-23.5)` → `23.5`                                   |
| *Conditional Functions*  | `CASE()`, `COALESCE()`, `NULLIF()`               | `COALESCE(email, 'No Email')`<br>`NULLIF(status, 'Inactive')`<br>`CASE WHEN sales > 100 THEN 'High' ELSE 'Low' END` |

<aside>

💡 The above table is incomplete and more functions can be found in the SQL documentation.

</aside>