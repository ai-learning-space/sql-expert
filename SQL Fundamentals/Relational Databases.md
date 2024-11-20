# Relational Databases🔗

Relational databases *(RDB)* are one of the most common ways of storing and organizing data. Their main advantage is that the data is organized into tables, where each row is a record, and the columns are the attributes of the data. This structure provides flexibility and the ability to easily search and manipulate data using the SQL language.

<aside>

📖 **Relational Databases** — based on the relational model, where data is organized into tables containing rows and columns

</aside>

Each row in a table is always unique (i.e. there is no sense storing duplicate data). For this purpose, each table must always have a special column to identify each record called *Primary Key 🔑* 

<aside>

📖 **Primary Key** — unique identifier for each record in a table

</aside>

Relationships between tables are created using *Foreign Keys*, which allow you to link data from different tables.

<aside>

📖 **Foreign Key** — column or set of columns in one table that references the **Primary Key** in another table

</aside>

# Relational Database Example 🧪

Let’s have a look at example of *“Car Data Base”* that describes relationship between cars and owners 🚗👨‍💼

![relational-db](https://raw.githubusercontent.com/WebOfRussia/sql-course/refs/heads/main/SQL%20Fundamentals/img/relational-db.png)

The database consist of 3 tables:

- `Cars` → car related information (manufacture, name, …)
- `Owners` → owners related information (name, home address, …)
- `Ownership` → links `Cars` and `Owners` tables to track who owns what cars

Besides it has the following *Primary Keys:*

- `Cars.ID` , `Ownership.ID` , `Owners.ID`

*Foreign Keys:*

- `Ownership.CarID` , `Ownership.OwnerID`

# Features of Relational Databases 💡

- The data structure in relational databases is pre-defined and strictly typed.
- Data is stored in the form of tables consisting of rows and columns.
- Only one value can be at the intersection of a row and a column.
- Each column has its own name and a clearly defined data type, which all values in this column must correspond to.
- The order of the columns is specified when creating a table and remains fixed.
- The results of SQL queries are returned as tables.

# Advantages ⚡

- *Structured Data and ACID Compliance*:
    - Enforce a structured schema, ensuring data is organized in tables with defined relationships. They follow *ACID (Atomicity, Consistency, Isolation, Durability)* principles, which guarantee reliable transactions and data integrity.
    - This makes them ideal for applications where data consistency and accuracy are critical, such as *financial systems* or *inventory management*.
- *Powerful Querying with SQL:*
    - Use *Structured Query Language (SQL)* for querying and manipulating data, offering a powerful and flexible way to perform complex queries, joins, and aggregations.
    - Users can easily retrieve and analyze data from multiple tables, enabling advanced reporting and data analytics

# Disadvantages 📉

- *Scalability Challenges:*
    - May face challenges when scaling horizontally (adding more servers), as they are typically designed to run on a single server or require complex sharding to distribute data across multiple servers.
    - It limits their performance and flexibility for applications that need to handle large volumes of data or high traffic loads.
- *Fixed Schema:*
    - The predefined *schema* of relational databases can make it difficult to adapt to changing requirements. Altering the *schema*, such as adding new fields or changing relationships, can be complex and time-consuming.
    - This hinders development agility, especially in fast-paced environments where requirements may evolve frequently.
- *Complexity of Relationships:*
    - While relational databases manage relationships well, they can become complicated in scenarios involving many-to-many relationships, requiring additional tables (junction tables) and more complex queries.
    - This complexity can lead to performance issues and make it harder to write and maintain queries, particularly for less experienced users.

# Popular Relational Databases ❤️

Here is a list of relational databases that exists in real world:

- ***PostgreSQL***
    - PostgreSQL is an advanced open-source relational database known for its robustness, extensibility, and compliance with SQL standards. It supports complex queries, *ACID* transactions, and offers features like *JSON* support, full-text search, and custom data types.
- ***Oracle***
    - Oracle Database is a high-performance, enterprise-grade relational database management system *(RDBMS)* developed by Oracle Corporation. It provides advanced features like partitioning, clustering, and high availability, and is known for handling large-scale applications and critical workloads.
- ***MySQL***
    - MySQL is a widely-used open-source relational database, known for its simplicity, speed, and efficiency. It’s commonly used for web applications and supports basic SQL functionalities with optional advanced features.

For your PET-project *MySQL* or *PostgreSQL* is sufficient. For example, *MySQL:*

- Lightweight and easy to lean
- Great choice for small-scale or personal projects
- Extensive documentation and community support