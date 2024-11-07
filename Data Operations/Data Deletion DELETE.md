# Data Deletion | DELETE

# Data Deletion | DELETE 🗑️

The data might become irrelevant at some point be deleted. In this case, use `DELETE`

<aside>
📖

**DELETE** — is used to remove rows from a table

</aside>

# DELETE Syntax **⚙️**

`DELETE` has the following syntax:

```sql
DELETE FROM table_name
WHERE condition;
```

<aside>
💡

`WHERE` is important. If `WHERE` is missing, all rows will be deleted!

</aside>

# DELETE Example 🧪

Let’s simply delete a one passenger:

```sql
DELETE FROM passenger
WHERE name = "Jane Smith";
```

# TRUNCATE vs DELETE

In some cases, you might hear about *TRUNCATE*. The `TRUNCATE` statement is similar to `DELETE`, but it removes all rows from a table more efficiently:

```sql
TRUNCATE TABLE students;
```

<aside>
💡

`TRUNCATE` is faster because it doesn't log individual row deletions.

</aside>

# When to Use DELETE? **🤔**

- *Removing Old Data:*
    - You may need to remove outdated records to keep the database clean.
- *Data Correction:*
    - When you accidentally insert wrong data, the `DELETE` statement helps remove those incorrect rows.
- *User Data Removal:*
    - In cases like user account deletions, the `DELETE` statement is used to remove the user’s data from relevant tables.

# Important Notes **⚠️**

- *Test with a `SELECT` First:*
    - Before running a `DELETE`, execute a `SELECT` query with the same `WHERE` clause to ensure it only affects the intended rows.
- *Back Up Data*:
    - For important data, create a backup before executing a `DELETE` statement, especially if it’s a bulk delete.
- *Be Aware of Foreign Keys:*
    - If a table has foreign key constraints, you might need to delete related rows in other tables first or use `ON DELETE CASCADE` in your table schema.
- *Caution with DELETE:*
    - The `DELETE` statement permanently removes data from the table. Once deleted, the rows cannot be recovered unless the database has backups or a rollback feature is used (like in transactions).
- *Deleting Large Datasets:*
    - For very large datasets, deleting many rows at once can be slow. Sometimes it’s more efficient to delete rows in smaller batches.