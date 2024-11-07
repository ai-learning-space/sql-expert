# DBs Creation/Deletion

# Creating Databases 🌱

When writing SQL queries, we actively use tables. These *tables* are stored within specific *databases*, which is the focus of this article. The syntax for creating a *database* is as follows:

```sql
CREATE DATABASE database_name;
```

*Database* names can consist of letters, numbers and the symbols `"_"` and `"$"`. A name may start with numbers but cannot consist solely of them. The maximum length for a name is 64 characters. You may provide additional parameters during database creation:

- *Owner*: You can specify the owner of the database using the `OWNER` clause.
- *Encoding*: You can set the character encoding for the database using the `ENCODING` clause.
- *Template*: You can also create a database based on an existing template database.

```sql
CREATE DATABASE my_database
		WITH OWNER my_user
				ENCODING 'UTF8' 
        TEMPLATE template0 
        CONNECTION LIMIT 100;
```

You can verify the creation of a database using the `SHOW DATABASES` command:

```sql
SHOW DATABASES;
```

# Deleting Databases 💥

To delete an existing database, you can use the `DROP DATABASE` command.

```sql
DROP DATABASE database_name;
```

# Using the IF [NOT] EXISTS 🛠️

When creating or deleting a *database*, errors can occur if a database with the same name already exists (when creating) or if the database doesn’t exist (when deleting). To handle these situations, the `IF [NOT] EXISTS` clause can be used. If you want to create a *database* only if it doesn’t already exist, you would use the following syntax:

```sql
CREATE DATABASE IF NOT EXISTS database_name;
```

If you want to delete a database only if it exists, the following syntax should be used:

```sql
DROP DATABASE IF EXISTS database_name;
```