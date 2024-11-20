# SQL Query Syntax ⚙️

At the very beginning we need to learn the fundamental principles and structures of SQL. We'll start by exploring the basic components of SQL queries including: `SELECT` , `FROM` , `WHERE` , `JOIN` to help you extract meaningful insights from your data.

# Data Selection | SELECT 🗂️

Data that is stored in a database has lots of different columns and there is no need to always select all columns. There are many reasons for it, starting from inefficiency and ending by irrelevant information that we simply don’t need, to select only information that we need (e.g. person name, email and address) we use `SELECT` operator.

The `SELECT` statement is one of the most fundamental components of SQL and is essential for retrieving data from databases. Here’s a breakdown to help you understand how to use the `SELECT` statement effectively:

```sql
SELECT column1, column2, ... 
FROM table_name;
```

<aside>

💡
- `SELECT` ****—**** keyword is used to specify the columns you want to retrieve
- `FROM` — keyword indicates the table from which to retrieve the data

</aside>

Let’s select several columns from *“Booking”* table:

```sql
SELECT name, email, phone_number	
FROM booking;
```

### All Columns Selection

If you want to retrieve all columns from a table, you can use the asterisk `*` wildcard:

```sql
SELECT * FROM table_name;
```

To retrieve all columns from *“Booking”* table:

```sql
SELECT *	
FROM booking;
```

Besides, you can retrieve custom/arbitrary strings, numbers, dates, …

```sql
SELECT "Hi, I’m learning SQL", 999;
```

<aside>

💡 `SELECT` can retrieve not only data rom database tables but also to display arbitrary strings, numbers, dates, and more. 

</aside>

# Aliases 🏷️

Oftentimes we would like to rename columns that we get from the queries. For example, product manager in our team would like to see a nice report that is understandable and nice to read but in the database we have columns that don’t convey the meaning and it’s hard to understand for non-technical people. 

In this case we may use *aliases*. *Aliases* in SQL are temporary names that you can assign to database tables or columns within a query. They are particularly useful for enhancing the readability of your SQL statements, simplifying complex queries and providing more meaningful labels for the results in your output. Aliases are defined by using `AS` keyword:

```sql
SELECT column1 AS name1, column2 AS name2, ...
FROM table_name;
```

For example, in our *“Booking”* table let’s retrieve the information about a user:

```sql
SELECT
    name AS client_name,
    email AS client_email,
    phone_number AS client_phone_number
FROM booking;
```

Now the output will be more pretty and understandable.

<aside>

💡 *Aliases* can be used not only for columns but for tables as well. Besides, `AS` is optional and can be omitted. However, it’s recommended to explicitly define it to keep the code understandable and consistent.

</aside>

```sql
-- not recommended 
SELECT
    name client_name,
    email client_email,
    phone_number client_phone_number
FROM booking;
```

*Aliases* are a valuable feature that can significantly enhance the clarity and efficiency of your queries. By using aliases effectively, you can make your SQL code more readable and user-friendly, ensuring that your data analysis is both efficient and comprehensible. In practice, you’ll find that leveraging *aliases* can greatly improve your SQL querying experience!

<aside>

💡
   - *Aliases* don’t change the actual table or column names in the database
   - Always use *aliases* when your queries involve multiple tables or function calculations

</aside>