# Operator REGEXP 🗒️

Sometimes string columns might be so different and complex that even with operator `LIKE` you will be unable to solve your task. In this case you can use more advanced approach called *regular expressions*.

<aside>

📖 `REGEX` is used to perform advanced pattern matching within string data.

</aside>

It allows you to search for specific patterns, extract information or even replace certain parts of a string. While SQL itself provides some basic string matching tools like `LIKE`, `REGEXP` offers much more flexibility and power when working with complex patterns.

# REGEXP Logic 🧩

Many SQL databases, such as *MySQL*, *PostgreSQL* and *Oracle* support *regular expressions*. The syntax might slightly differ, but the general idea is consistent. *Regular expressions* use a series of symbols to define patterns for searching within strings. 

```sql
-- REGEXP synatx
... WHERE table_field REGEXP 'pattern';
```

For example, in *“Air Travel”* database we have different planes (e.g. *Boeing 737, Airbus A320, Bombardier CRJ900).* Let’s select only those records that have a plane that have only 3 numbers in name:

```sql
SELECT *
FROM planes
WHERE model REGEXP '[0-9]{3}';
```

# REGEXP or LIKE? 🤔

The `LIKE` operator is convenient for simple search patterns, such as finding strings that start or end with a specific set of characters or contain certain substrings. However, if more complex and flexible searching is required — such as searching with multiple conditions or using special characters and ranges — the `REGEXP` operator becomes an indispensable tool.

<aside>

💡 Use `REGEXP` when complex and flexible searching is required!

</aside>

# Regular Expression Syntax ⚙️

- **Case Insensitivity**
    - By default, regular expressions in are *case-insensitive*. The expression `REGEXP 'abc'` will find strings like `abc`, `Abc`, and `ABC`.
- **Escape Characters**
    - Certain characters have special meanings in regular expressions and require escaping (e.g. **, +, ?, [, ], (, ), {, }, |, \*). The backslash `\\` is used for escaping.

# Special Characters and Structures 📜

| **Characters/Structures** | **Description** |
| --- | --- |
| `*` | 0 or more instances of the preceding string |
| `+` | 1 or more instances of the preceding string |
| `.` | Any single character |
| `?` | 0 or 1 instance of the preceding string |
| `^` | Matches the beginning of the string |
| `$` | Matches the end of the string |
| `[abc]` | Any character listed in the brackets |
| `[^abc]` | Any character not listed in the brackets |
| `[A-Z]` | Matches any uppercase letter from the Latin and Cyrillic alphabets, respectively |
| `[a-z]` | Matches any lowercase letter from the Latin and Cyrillic alphabets, respectively |
| `[0-9]` | Matches any digit |
| `p1` | p2 |
| `{n}` | n instances of the preceding string |
| `{m, n}` | Between m and n instances of the preceding string |

# REGEXP Examples 🧪

To get all users whose names start with *"John"*:

```sql
SELECT * 
FROM passenger
WHERE name REGEXP '^Jennifer';
```

The expression searches for strings that start with `Jennifer` The symbol `^` indicates the beginning of the string. Now let's retrieve all names that end with either letter `h` or `s` :

```sql
SELECT *
FROM flight
WHERE name REGEXP '[hs]$';
```

In this example, `[hs]` defines the list of possible values for the pattern, `$` indicates what the string should end with. Now, let's find all users that travelled either on `Boeing 737` or `Boeing 777` :

```sql
SELECT * 
FROM passenger
WHERE plane_name REGEXP 'Boeing (737|777)$';
```

# Important Notes ⚠️

- `REGEXP` offers powerful search capabilities far beyond than `LIKE`
- *Regular expressions* are highly flexible, allowing complex search criteria like multiple conditions, ranges of characters or repeated patterns.
- While `REGEXP` can be very efficient, it can also be computationally expensive for large datasets, so use it wisely when performance is a concern.