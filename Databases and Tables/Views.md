# Views 🖼️

Well-designed applications often provide a public interface that hides implementation details, allowing for design changes without impacting end users. When designing your *database*, you can achieve a similar outcome by concealing tables and granting access to data exclusively through a set of *views*.

# What is a View? 🤔

<aside>

📖 **View** — is a database object that represents the result of a query executed against the database, defined using a `SELECT` statement at the time the view is accessed.

</aside>

*Views* are sometimes referred to as *"virtual tables"* because they appear to users as tables.

<aside>

💡 Views don’t store data themselves. They retrieve data from other tables when are used.

</aside>

If the data in the underlying table changes, the user receives updated information when accessing the view that utilizes that table. 

<aside>

💡 Views don’t cache the results of queries.

</aside>

# View Syntax ⚙️

A *view* is created by using the following syntax:

```sql
CREATE [OR REPLACE] VIEW view_name [(view_field_names)] AS select_expression
```

The optional `OR REPLACE` clause allows you to replace an existing *view* with the same name, removing the old *view* and creating a new one. Without this clause, an error will occur if you attempt to create a *view* with an existing name.

# View Example 🧪

As a simple example, let's assume you want to partially hide *email addresses* in the *Users* table. This can be particularly useful if your company's policy restricts access to sensitive user information. 

Instead of granting direct access to the *Users* table, you define a view named `ViewUsers` and require everyone to use it to access user data. Here’s an example of how to define this view:

```sql
CREATE VIEW ViewUsers AS
    SELECT id,
    name,
    CONCAT(SUBSTR(email, 1, 2), '****', SUBSTR(email, -4)) AS email
FROM Users;
```

Now we can query the created view:

```sql
SELECT * FROM ViewUsers;
```

If you want to find out which columns are available in a view, you can use the `DESCRIBE` statement:

```sql
DESCRIBE ViewUsers;
```

This will return:

```
Field      Type          Null    Key     Default    Extra
id         int           NO              <NULL>
name       varchar(32)   NO              <NULL>
email      varchar(38)   YES             <NULL>
```

# Why Use Views?🤔

- ***Simplifying Complex Queries:***
    - *Views* are used to simplify complex queries and create an abstraction layer between the user and the database. They can hide the complexity of the data structure and provide a streamlined interface for data access.
- ***Improving Performance:***
    - Creating *views* that encapsulate complex queries can help optimize the execution of those queries, leading to faster query execution and improved overall database performance.
- ***Enhancing Security:***
    - *Views* can be employed to secure sensitive data. By creating views that restrict access to specific columns or rows, administrators can limit exposure to confidential information, ensuring that only authorized users have access to sensitive data.