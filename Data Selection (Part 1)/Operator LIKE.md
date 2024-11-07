# Operator LIKE

# Operator LIKE 👯

The data quite often contains text that may have different patterns. 

<aside>
📖

`LIKE` operator in SQL is used to search for a specified pattern in a string column

</aside>

It is especially useful when you need to filter data based on partial matches or when you’re looking for rows where the column contains a specific substring.

Suppose we want to find all users whose *email* is in the second-level domain *"gmail".* This is a bit complicated since length of a string is always different and may contain unexpected characters. For such use-cases, `LIKE` is well-suited.

# **LIKE Syntax ⚙️**

```sql
... WHERE column_name [NOT] LIKE string_pattern
```

The *pattern* can include the following special characters:

| **Symbol** | **Description** |
| --- | --- |
| `%` | A sequence of any characters (the number of characters can be 0 or more) |
| `_` | Any single character |

Let’s come back to our previous example and select users that have “*gmail"* domain:

```sql
SELECT name, email
FROM client
WHERE email LIKE '%@gmail.%';
```

Let’s understand what was going on the query above:

- The **`%`** wildcard represents zero or more characters, meaning it can match any sequence of characters. We allow having any text at the beginning of a string and after `@gmail.`
- The `@gmail.` portion indicates that the email must contain the string `@gmail.` after any preceding characters.

# **LIKE Examples** 🧪

let’s have a look at more examples with `LIKE` operator:

| **SQL Query** | **Description** |
| --- | --- |
| `... WHERE column_name LIKE 'text%’` | Matches any strings that begin with `"text"` |
| `... WHERE column_name LIKE '%text’` | Matches any strings that end with `"text"` |
| `... WHERE column_name LIKE '_ext’` | Matches strings that are 4 characters long, with the last 3 being `"ext"` Examples include `"text"` and `"next"` |
| `... WHERE column_name LIKE 'begin%end’` | Matches strings that start with `"begin"` and end with `"end"` |

# **ESCAPE Character 🏃‍♂️**

The *ESCAPE* character is used to escape special characters → `%` and `\`. If you need to find strings that include these characters, you can use the *ESCAPE* character. For example, if you want to get job *IDs* where the progress is `3%`:

```sql
SELECT job_id FROM Jobs
WHERE progress LIKE '3!%' ESCAPE '!';
```

If we did not escape the wildcard character, the selection would include everything starting with 3.