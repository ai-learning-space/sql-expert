# Data Update | UPDATE 🔄

The data that is already exists might be updated from time to time. In this case, use `UPDATE`.

<aside>

📖 **UPDATE** — is used to modify existing data in a table.

</aside>

Instead of inserting new rows, it allows you to change the values of one or more columns in the rows that match a given condition. Operator `UPDATE` has the following simple syntax:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

<aside>

💡 `WHERE` is important since it determines what rows to update. If `WHERE` is omitted, all rows will be updated (dangerous).

</aside>

# UPDATE Example 🧪

let’s update price for apartments with type *“Entire home/apt”* by 100:

```sql
UPDATE apartment
SET price = price + 100
WHERE type = "Entire home/apt";
```

# When to Use WHERE? 🤔

- ***Correcting Data:***
    - When a mistake has been made in the data, such as a wrong name or date, the `UPDATE` statement allows you to correct it.
- ***Adjusting Data:***
    - If you need to apply changes across multiple records based on certain conditions, like updating the status of users or modifying prices.

# Important Notes ⚠️

- ***Always Use `WHERE` Clause:***
    - If you don’t want to update all rows in a table, include a `WHERE` clause. Accidentally updating all rows is a common issue if the `WHERE` clause is omitted.
- ***Backup Critical Data:***
    - Before running an `UPDATE`, especially for large data sets or in production, consider backing up the data or testing the update on a subset of the data.
- ***Use Transactions:***
    - In systems that support transactions, such as *PostgreSQL* and *MySQL*, wrap the `UPDATE` statement in a transaction. This allows you to roll back if something goes wrong.