# Transaction Creations

# Creating Transactions 💳

If you attempt to transfer $1,000 from your savings account to your checking account and suddenly find that the money was deducted but not credited to your checking account, you would likely be upset.

To protect against such errors, the program processing your money transfer request first initiates a transaction, then executes the necessary SQL queries to transfer money from one account to another. If everything goes well, the transaction is completed with a `COMMIT` command, which saves the changes.

However, if any issues arise, the `ROLLBACK` command is executed, instructing the server to undo all actions taken since the start of the transaction.

<aside>
💡

- `COMMIT` — is used to apply changes in a transaction
- `ROLLBACK` — is used to undo changes in a transaction
</aside>

The process might look like this:

```sql
-- start the transaction
START TRANSACTION;

-- check if the sender has sufficient balance
SELECT @balance := user_balance FROM accounts WHERE user_id = 1;

-- Iif insufficient funds, rollback the transaction
IF @balance < 1000 THEN
    ROLLBACK;
END IF;

-- check for the existence of the recipient
SELECT @exists := COUNT(*) FROM accounts WHERE user_id = 2;
IF @exists = 0 THEN
    ROLLBACK;
END IF;

-- update account balances if all checks pass
UPDATE accounts SET user_balance = user_balance - 1000 WHERE user_id = 1;
UPDATE accounts SET user_balance = user_balance + 1000 WHERE user_id = 2;

-- apply the changes
COMMIT;
```

With the transaction in place, the program ensures the safety of your $1,000, guaranteeing that it either remains in the original account or is transferred to another account, thus eliminating the risk of loss.

# Starting and Ending Transactions 🏁

Each explicit transaction in MySQL begins with the `START TRANSACTION` statement.

A transaction can be concluded in two ways:

- *Using the COMMIT command*, which instructs the server to mark the changes as permanent and release all resources (i.e., row locks) used during the transaction.
- *Using the ROLLBACK command,* which tells the server to revert the data to its state before the transaction began. After the rollback, any resources used by the transaction are also released.

In addition to the `COMMIT` and `ROLLBACK` commands, a transaction may also conclude due to external factors. For instance, if the server shuts down, your transaction will be automatically rolled back when the server restarts.

# Savepoints in Transactions 📝

In certain situations, you may need to roll back within a transaction without canceling all the work done. To achieve this, you can set one or more savepoints within the transaction. This allows you to roll back to a specific point in the transaction rather than the beginning.

Each savepoint in a transaction must be assigned a unique name, allowing for multiple different savepoints. To create a savepoint called `my_savepoint`, use the following command:

```sql
SAVEPOINT my_savepoint;
```

To roll back to a specific savepoint, simply enter the `ROLLBACK` command followed by the keywords `TO SAVEPOINT` and the savepoint name, for example:

```sql
START TRANSACTION;

-- create a savepoint before updating the balance of the first user
SAVEPOINT before_updating_user_1;
UPDATE accounts SET balance = balance + 100 WHERE user_id = 1;

-- check the condition for the first user
-- for instance, verify business logic

-- here we assume that the condition failed, and we need to revert the balance change
ROLLBACK TO SAVEPOINT before_updating_user_1;

-- update the balance for the second user
UPDATE accounts SET balance = balance + 200 WHERE user_id = 2;

-- conclude the transaction
COMMIT;
```

As a result of this transaction, the first user's balance remains unchanged due to the rollback to the savepoint, while the second user's balance increases by 200. This demonstrates how to manage changes in the database with a high level of control using transactions and savepoints.

When using savepoints, keep in mind the following points:

- Despite the name, creating a savepoint does not save anything. To make your changes within the transaction permanent, you must execute the `COMMIT` command.
- When rolling back a transaction without specifying a particular savepoint, all previously set savepoints will be ignored, and the entire transaction will be rolled back.