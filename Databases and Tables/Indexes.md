# Indexes

<aside>

💡 By default, DBMS doesn’t place the data in an optimal order.

</aside>

For example, when adding a row to the Users table, the *DBMS* doesn’t arrange the rows in numerical order based on the `id` column or in alphabetical order based on the `last_name` column. Instead, it simply places the data in the next available space in the file (the *DBMS* maintains a list of free spaces for each table). When we execute the query:

```sql
SELECT email FROM Users WHERE email LIKE 'l%';
```

Requires the database server to check each row in the table to find matches. This approach works fine for small tables but becomes overly time-consuming as the data volume grows.

# Comparing Query Performance with and without Indexes

*Indexes* function like subject pointers in a book, allowing quick information retrieval without reading through all the text. They are special tables where the rows, unlike regular data tables, are arranged in a specific order. However, instead of containing all the data about a record, an index holds only the column(s) used to find rows in the data table, along with information that describes where that row is physically located. Therefore, the role of indexes is to facilitate searching for subsets of rows and columns without needing to scan every row in the table.

# Creating an Index ✨

Returning to the Users table, you can add an index to the `email` column to speed up any queries that utilize this column's value.

Here’s how to add such an index in MySQL:

```sql
CREATE INDEX idx_email ON Users (email);
```

This command creates an index named `idx_email` for the `Users.email` column. With the index in place, the query optimizer can decide to use the index if it deems it beneficial. If there are multiple indexes in the table, the optimizer must determine which index is the most advantageous for a particular SQL statement.

All database management systems provide a way to view existing indexes. For MySQL users, the `SHOW` command can display all indexes for a specific table, as shown in the example below:

```sql
SHOW INDEX FROM Users;
```

```
Table      Non_unique  Key_name      Seq_in_index  Column_name
users      0           PRIMARY       1             id
users      1           idx_email     1             email

```

The output demonstrates that the Users table has two indexes: one for the `id` column named `PRIMARY` and another for the `email` column that we just defined.

When the table was created, MySQL automatically generated an index for the primary key column, which in this case is `id`, and assigned the index the name `PRIMARY`. This is a special type of index used with primary key constraints, ensuring that each value in the column or group of columns designated as the primary key for the table is unique and cannot be NULL.

# Dropping an Index

If you decide that an index is no longer needed after creating it, you can remove it like this:

```sql
DROP INDEX idx_email ON Users;
```

# Unique Indexes

When designing databases, it's important to determine which columns allow duplicate values and which do not.

For instance, in the Users table, multiple users may have the same names, but their identifiers and email addresses must be unique for differentiation.

You can achieve guaranteed uniqueness of values by creating a unique index on the `Users.email` column. A unique index serves two functions:

1. It provides all the benefits of a standard index.
2. It prevents duplicate values in the indexed column.

The database management system will check the unique index when attempting to add or modify data in the indexed column to ensure that the entered value does not duplicate an existing value in the table.

Creating a unique index for the `Users.email` column is done as follows:

```sql
CREATE UNIQUE INDEX idx_email ON Users (email);
```

With this index in place, you'll receive an error message if you try to add a new user with an already existing email address:

```
Error(1062) 23000: "Duplicate entry 'duplicate@gmail.com' for key 'users.idx_email'"
```

Creating unique indexes for columns or groups of columns defined as primary keys is redundant since the database management system automatically ensures the uniqueness of primary key values. However, having multiple unique indexes in a table is permissible and can be advisable if needed.

# Multi-Column Indexes

In addition to single-column indexes, you can also create indexes that include multiple columns. For example, to search for students by both their first and last names, you can create a composite index on these two fields:

```sql
CREATE INDEX idx_full_name ON Student (last_name, first_name);
```

This index will be useful for queries that require both the first and last names or just the last name. However, it will not benefit queries that only specify the first name. It’s similar to searching for a phone number in a phone book: if both the first and last names are known, the search is simplified due to the ordering of the directory by last name and then by first name. If only the first name is known, you'll need to sift through all entries to find the right person.

When creating multi-column indexes, it's crucial to consider the order of the columns in the index to maximize efficiency. However, to achieve the desired query performance, you can always create multiple indexes with the same columns but in different orders.

# How Indexes Are Used

Indexes are often utilized by the DBMS to efficiently search for specific rows in a table and then retrieve additional data from related tables based on user queries. For example, consider the query:

```sql
SELECT id, first_name, last_name
FROM Student
WHERE first_name LIKE 'A%' AND last_name LIKE 'L%';
```

In response to this query, the DBMS may choose one of several approaches:

1. Perform a full scan of all rows in the table.
2. Use the index on the `last_name` column to find students with last names starting with "L," then check each of those rows for first names starting with "A."
3. Use the composite index on `last_name` and `first_name` to directly find students that meet both criteria.

The last method is the most efficient, as it allows finding all necessary rows in one pass, avoiding additional access to the table. But how can you determine which method the MySQL query optimizer will choose? You can use the `EXPLAIN` command, which shows how the DBMS plans to execute the query without actually running it:

```sql
EXPLAIN
SELECT id, first_name, last_name
FROM Student
WHERE first_name LIKE 'A%' AND last_name LIKE 'L%';
```

The output will look something like this:

```
id  select_type  table   partitions  possible_keys             key
1   SIMPLE       Student <NULL>     idx_full_name,idx_last_name idx_full_name
```

Analyzing the results, you can see that the `possible_keys` column lists potential applicable indexes (`idx_last_name` or `idx_full_name`), while the `key` column indicates that the `idx_full_name` index was chosen.

# The Downside of Indexes

If indexes are so effective, one might wonder why not simply index everything?

The answer lies in the fact that each index is a table (albeit a special type of table). Therefore, every time a row is added to or removed from the table, all indexes in that table must be updated. When a row is updated, any indexes for the affected column(s) must also be modified. Consequently, the more indexes you have, the more work the DBMS must do to keep all schema objects up to date, leading to a slowdown in performance.

Moreover, indexes take up additional disk space and require careful management by database administrators. Therefore, the optimal strategy is to create indexes only when truly necessary. If an index is needed temporarily, such as for generating a monthly report, it can be added before the procedure begins and removed afterward.

Ultimately, the ideal approach is to find a balance: have enough indexes for efficient operation without overwhelming performance. If you're unsure how many indexes are needed, start with a minimal number and add more as necessary.