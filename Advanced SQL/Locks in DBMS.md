# Locking in DBMS 🔒

Database management systems allow a single user to retrieve and modify data. However, in today's world, thousands of people can make changes to a database simultaneously. If users primarily perform read operations, this load poses little challenge to the database server. But if some users are adding or modifying data concurrently, the server faces much more complex tasks.

Imagine you are preparing a financial report that summarizes daily store sales over the week. At the same time you are working on the report, the following operations occur:

- A customer purchases an item.
- Another customer returns a defective item and receives a refund.
- The store receives a new shipment of products.

During the time your report is being generated, multiple users are altering information in the database. So, what numbers should appear in the report? The answer depends on how your server handles locking.

# Locking 🔒

<aside>

📖**Locking** —  is a method of restricting access to data to ensure the correct processing of transactions

</aside>

Database servers use locks to manage concurrent access to data, ensuring that while one transaction is working with the data, other transactions cannot modify it. When data in the database is locked, other users who want to change or read that data must wait until the lock is released.

# Granularity of Locks ⚙️

There are several different strategies for how to lock a resource. The server can apply locks at one of three different levels, or granularities:

- *Table Locking:*
    - Prevents multiple users from simultaneously modifying data in the same table.
- *Page Locking:*
    - Prevents multiple users from modifying data on the same page (a page is a memory segment, typically ranging from 2 to 16 KB) of a table at the same time.
- *Row Locking:*
    - Prevents multiple users from simultaneously modifying the same row in a table.

These approaches have their advantages and disadvantages. Locking the entire table requires less overhead but can lead to long wait times as the number of users increases. Row locking requires more overhead but allows multiple users to modify the same table if they are working with different rows.