# Data Inserting | INSERT

# Data Inserting | INSERT ➕

Although querying already existing database is the most often task that we deal with, we do need to create either a table or even an entire database from scratch sometimes. 

<aside>
📖

**INSERT** — is used to add new rows of data into a table.

</aside>

This is fundamental for populating tables with data, whether adding single rows or bulk data entries. The `INSERT` statement can work with various syntax options, depending on the need to insert a single row, multiple rows or data derived from other queries. The basic syntax involves specifying the table where you want to insert the data, along with the values that correspond to each column.

# INSERT Syntax **⚙️**

Operator `INSERT` has the following syntax:

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

Besides, we can insert new values in the following ways:

- *Single/Multiple Row/Rows Inserting*
- *Inserting Data From Another Table*

# INSERT Example 🧪

For example, let’s insert a new record in a database:

```sql
INSERT INTO passenger
VALUES (1, 'Jane Smith');
```

Probably, if we execute the above query an error will occur. The reason for that is *id value*. If the database already exists, we cannot use *id=1* because there is already a record with such *id*.

<aside>
💡

If a column has `AUTO_INCREMENT` , you don’t need to specify a value for it. The database will automatically generate the next value.

</aside>

So we have to then write the following query:

```sql
INSERT INTO passenger
VALUES ('Jane Smith');
```

In the above query we inserted a new row but we didn’t specify the columns!

<aside>
💡

It’s always safer to specify inserting column names to avoid mistakes

</aside>

Let’s add several rows and use explicit columns definition:

```sql
INSERT INTO passenger (name)
VALUES
		 ('Mark Smith'),
		 ('Lisa Smith');
```

As it was mentioned above, new values can be inserted by using `SELECT` . It's useful when you want to copy data from one table to another or when the values you need to insert are derived from a query. 

```sql
INSERT INTO archived_passenger (name)
SELECT name
FROM passenger 
LIMIT 3;
```

<aside>
💡

If you don’t have data for a column, you can explicitly set it to `NULL` 

</aside>