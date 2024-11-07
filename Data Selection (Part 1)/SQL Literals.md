# SQL Literals

# Literals in SQL 🧮

Data Analysts quite often encounter situations when they have to provide fixed values in queries. In this cases they use *literals* to make their life easier. 

<aside>
📖

**Literals** — fixed values that are directly written into a query

</aside>

These values aren’t associated with any column or table and they represent constant data such as *numbers*, *strings* or *dates*. In SQL we usually have the following types of *literals*: *String, Numeric, Date and Time, Logical* and *NULL.* let’s have a look at them one by one.

# String Literals 🆎

<aside>
📖

**String Literals** — sequences of characters enclosed in single/double quotes

</aside>

String literals are usually used to represent text data, for example:

```sql
SELECT
		"This is string literal",
		'This is anohter string literal'
```

They are usually used in conjunction with `WHERE` to perform data filtering. For example, for *“Apartment”* table we may want to find only apartments that have specific property type:

```sql
SELECT *
FROM apartment
WHERE type = 'Private room'; -- 'Private room' is a string literal
```

# Numeric Literals 🔢

<aside>
📖

**Numeric Literals** — numerical values (integers or decimals)

</aside>

Numeric literals are usually used to represent numeric data, for example:

```sql
SELECT 777, 77.7, .9, 1e3
```

They used in conjunction with `WHERE` to perform data filtering as well:

```sql
SELECT *
FROM apartment
WHERE price >= 150; -- 150 is a numeric literal
```

The table below shows a bit more information about numeric literals:

| **Example** | **Explanation** |
| --- | --- |
| `2.3`, `6`, `0.09` | Includes *integer* and *float* numbers. The separator for a float number is `"."` |
| `1e3` , `1e5`  | Exponential form (e.g. `1e3` → `1000` ) |
| `.2` , `.9` , `1` | This format is allowed  |

# Arithmetic Literals ➗➕

<aside>
📖

**Arithmetic Literals** — any arithmetic expressions

</aside>

*Arithmetic literals* are usually used to represent arithmetic operations, for example:

```sql
SELECT
		100 + 0.5,
		25 % 5,
		3 * 6
```

Usually a*rithmetic literals* are used for data calculations. Foe example, let’s select *price* of an apartment and a price with 30% discount for *“Apartment”* table:

```sql
SELECT
		price AS price
		price - price * 0.3 AS price_with_discount -- '-' is an arithmetic literal
FROM apartment;
```

The table below shows a bit more information about a*rithmetic literals*:

| **Operator** | **Description** | **Example** |
| --- | --- | --- |
| `+` , `-` , `/` , `*` | Subtraction, Division, …  | `20 + 3` , `5 * 4` , `3 / 2` |
| `%` , `MOD`  | Modulus Division | `20 % 5 = 0`  |

# Date and Time Literals 📅

<aside>
📖

**Date and Time Literals** — specific dates or times

</aside>

*Date and time literals* are usually used to represent date and time data. The format may vary based on the database system but commonly follows the `"YYYY-MM-DD"` or *Integer* values:

|  | **Description** | **Format** |
| --- | --- | --- |
| 

*Date* | 

Interpreted as a date with time equal to zero
 | 
`YYYY-MM-DD`, `YYYYMMDD` , `YYYY, MM-DD`

e.g. `1996-03-23`
 |
| 
*Time* | 
Contains only time without a specific date | `hh:mm:ss`, `hh:mm`, `hh`, `ss`

e.g. `12:00` , `12:30:55`  |
| 
*Date and Time* | 
Date with the ability to set a specific time | `YYYY-MM-DD hh:mm:ss`, `YYYYMMDDhhmmss`

e.g. `1996-03-23 12:30:55` |

They often used for data filtering and date time operations. For example, let’s retrieve only those bookings that happened after *“2023-12-29”*  from *“Booking”* table*:*

```sql
SELECT *
FROM apartment
WHERE checkin_date > "*2023-12-29*"; -- "*2023-12-29*" is date literal
```

# Logical Literals 🧩

<aside>
📖

**Logical Literals** — `TRUE` or `FALSE` values

</aside>

Theses literals represent the truth or falsity of a statement. When a query is being interpreted, SQL converts them to numbers: `TRUE` and `FALSE` become `1` and `0` respectively.

For example, we can retrieve apartments that have kitchen:

```sql
SELECT *
FROM apartment
WHERE has_internen = TRUE; -- TRUE is logical literal
```

# **NULL 🤷‍♂️**

<aside>
📖

**NULL Literals** — represent “no data”

</aside>

*NULL literals* represent the absence of a value or unknown data in SQL. They are especially useful when dealing with *incomplete* or *missing data* and can help handle such cases more effectively.

For example, we can retrieve users that didn’t provide phone number:

```sql
SELECT *
FROM client
WHERE phone_number IS NULL; -- NULL is null literal
```