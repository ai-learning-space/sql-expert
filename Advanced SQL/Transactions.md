# Transactions

# Transactions 💳

If database servers operated flawlessly 100% of the time, if users always allowed programs to complete execution, and if applications never encountered fatal errors that halted processes, there would be little to discuss regarding concurrent access to databases.

However, such an ideal situation is unrealistic, which is why we need to consider mechanisms that allow multiple users to work with the same data. One of the key elements in addressing this challenge is the transaction.

<aside>
📖

**Transaction** — is a sequence of operations on a database that are executed as a single unit

</aside>

In this section, we will discuss transactions that enable the grouping of multiple SQL statements into one cohesive unit, ensuring that either all statements are executed successfully or none are executed at all.