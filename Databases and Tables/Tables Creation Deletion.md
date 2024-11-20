# Tables Creation/Deletion 🌱

Tables are fundamental structures that store data in rows and columns. Below are the steps and commands for creating and deleting tables in PostgreSQL.

# Creating Tables 🌱

Before creating a table, you need to select the database where the table will be stored. This is done using the `USE` statement:

```sql
USE database_name;
```

To create a new table in you can use the `CREATE TABLE` command:

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
    column_1 data_type,
    [column_2 data_type,]
    ...
    [column_n data_type,]
);
```

For example, let's create a `Users` table:

```sql
CREATE TABLE Users (
    id INT,
    name VARCHAR(255),
    age INT
);
```

Here, `INT` and `VARCHAR(255)` represent the data types for *numeric* and *string* values, respectively.

# Additional Column Definition Parameters 📚

The column definitions above are simplified. Besides the column name and its data type, you might sometimes need to add the following optional parameters:

- *PRIMARY KEY:*
    - Specifies one or more columns as the primary key.
- *FOREIGN KEY:*
    - Specifies one or more columns as the foreign key.
- *AUTO_INCREMENT:*
    - Indicates that the value in this column will automatically increase with each new record added. Each table can have at most one `AUTO_INCREMENT` column, and this parameter can only be applied to integer and floating-point types.
- *UNIQUE*:
    - Ensures that all values in this column are distinct across all records.
- *NOT NULL:*
    - Specifies that this column cannot contain NULL values.
- *DEFAULT:*
    - Defines a default value. This parameter does not apply to *BLOB*, *TEXT*, *GEOMETRY* and *JSON* types.

For our `Users` table, we can specify the following parameters:

```sql
CREATE TABLE Users (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    age INT NOT NULL DEFAULT 18
);
```

In this example:

- `id` → is a numeric field and serves as the primary key.
- `name` → is a string field with a maximum length of 255 characters and is required.
- `age` → is a numeric field with a default value of 18.

# Describing the Table 📊

To view the structure of the created table, you can use the `DESCRIBE` command:

```sql
DESCRIBE Users;
```

# Additional Table Definition Parameters 📚

In addition to column descriptions, you can specify other parameters when creating a table:

Next, you need to add a `company` field to the `Users` table, which will reference a record in the `Companies` table. The complete command for creating the `Users` table will look like this:

```sql
CREATE TABLE Users (
    id INT,
    name VARCHAR(255) NOT NULL,
    age INT NOT NULL DEFAULT 18,
    company INT,
    PRIMARY KEY (id)
);
```

To ensure that the `company` column contains an identifier that exists in the `Companies` table when new records are added to the `Users` table, a foreign key is used. Its syntax is as follows:

```sql
FOREIGN KEY (column_1, column_n)
REFERENCES foreign_table (foreign_column_1, foreign_column_n)
[ON DELETE action]
[ON UPDATE action]
```

The complete command for creating the table with a *foreign key* will be:

```sql
CREATE TABLE Users (
    id INT,
    name VARCHAR(255) NOT NULL,
    age INT NOT NULL DEFAULT 18,
    company INT,
    PRIMARY KEY (id),
    FOREIGN KEY (company) REFERENCES Companies (id)
);
```

With *foreign keys*, you can define the behavior of the current record when the referenced record is modified or deleted:

```sql
CREATE TABLE Users (
    id INT,
    name VARCHAR(255) NOT NULL,
    age INT NOT NULL DEFAULT 18,
    company INT,
    PRIMARY KEY (id),
    FOREIGN KEY (company) REFERENCES Companies (id)
    ON DELETE RESTRICT ON UPDATE CASCADE
);
```

`ON DELETE RESTRICT` means that if you try to delete a company that has related data in the `Users` table, the database will not allow it:

```
Cannot delete or update a parent row: a foreign key constraint fails
```

If you specify `ON DELETE CASCADE`, deleting a company will also delete all users associated with that company. Another option is `ON DELETE SET NULL`. Using this, the database will set the `company` field to NULL for all users who worked at the deleted company.

`ON UPDATE CASCADE` means that if a company changes its identifier, all users will receive the new identifier in the `company` field.

# Deleting a Table 💣

To delete a table, you use the `DROP TABLE` command:

```sql
DROP TABLE [IF EXISTS] table_name;
```