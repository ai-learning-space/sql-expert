# Key-Value Databases 🔑

Key-value databases are one of the simplest and most efficient types of *NoSQL* storage. These databases organize data into *key-value* pairs, where each unique key corresponds to a specific value. This approach allows for fast access and manipulation of data, making *key-value* databases ideal for high-performance applications and scenarios that require scalability.

<aside>

📖 **Key-Value Database** — data storage where each record is represented as a key-value pair

</aside>

The *key* is a *unique identifier* for each value in the database, which means you can find any value by using its key. Both keys and values can be different types of data, including simple numbers and text, as well as more complex objects.

# Key-Value Database Example 🧪

For example, the below picture demonstrates *“Car”* database in key-values format:

![kvdb](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/SQL%20Fundamentals/img/kvdb.png)

We always have keys that may have flexible structure (e.g. *“name:id:attribute”) and values:*

![user-vs-kvdb](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/SQL%20Fundamentals/img/user-vs-kvdb.png)

# Primary/Foreign Keys 🗝️

*Key-value* databases don’t support the direct concept of *primary/foreign keys*, as there are no strict relationships between tables as in relational systems. However, it is possible to create references to other values using the key structure.

<aside>

📖 **Key-Value Database** no longer have strict format. Each entity may have its own structure

</aside>

Imagine you have a *key-value* database for a library. You might store information about books and authors like this:

```sql
-- Book 
Key: book:1
Value: {"title": "1984", "author_id": "author:1"}

-- Author
Key: author:1
Value: {"name": "George Orwell", "birth_year": 1903}
```

In this example, the book’s value includes a reference to the *author’s ID →* `author_id` , allowing you to link the book to its author, even without strict *foreign key* relationships.

<aside>

💡 You can retrieve the author’s details using the key `author:1` 

</aside>

# Advantages ⚡

- *High Speed* → fast access to data due to the simple key-value structure.
- *Simple Storage Model* → data is stored in a minimalistic form of pairs.
- *Flexibility* → values can be any data type, including complex formats such as *JSON*.

# Disadvantages 📉

- *Data Model Complexity* → poor scalability as the complexity of data models increases.
- *Multiple Records* → it is difficult to perform operations on several records at once.
- *No Query Language* → the logic that is usually implemented in the database must be transferred to the application code, which complicates its development and maintenance

# Popular Key-Value Databases ❤️

- ***Redis***
    - An in-memory data store that supports a variety of data structures such as strings, lists, sets, and hashes. Known for its speed and ability to handle real-time applications.
    - *Use cases* **→** Caching, session management, real-time analytics, messaging.
- ***Amazon DynamoDB***
    - A fully managed, serverless key-value and document database designed by AWS, offering high performance at any scale.
    - *Use cases* **→** Web applications, IoT, gaming, mobile backends, scalable applications.
- ***Memcached***
    - A distributed memory object caching system that speeds up dynamic web applications by reducing database load.
    - *Use cases* **→** Caching, session storage, quick lookups of temporary data.
- …