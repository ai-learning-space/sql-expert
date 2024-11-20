# Data Type Change | CAST

<aside>

📖**CAST** function is used to convert an expression from one data type to another.

</aside>

<br>

This is particularly useful when you need to ensure that data types match in operations, such as when performing calculations, comparisons or when inserting data into a table.

# CAST Syntax ⚙️

Operator `CAST` has the following syntax:

```sql
CAST(expression AS target_data_type);
```

Here’s a summary table of *Common Use Cases for the CAST Function* in SQL:

| **Use Case** | **Description** | **Example** | **Result** |
| --- | --- | --- | --- |
| *String to Integer* | Convert a string representation of a number to an integer. | `SELECT CAST('123' AS INT);` | `123` |
| *Integer to String* | Convert an integer to a string for concatenation or display. | `SELECT CAST(456 AS VARCHAR(10));` | `'456'` |
| *String to Date* | Convert a string in date format to a `DATE` type. | `SELECT CAST('2024-10-22' AS DATE);` | `2024-10-22` |
| *Floating-Point to Integer* | Convert a floating-point number to an integer (rounding down). | `SELECT CAST(123.45 AS INT);` | `123` |
| *Handling Null Values* | Convert `NULL` values to a specific type to avoid errors. | `SELECT CAST(NULL AS VARCHAR(20));` | `NULL` |
| *Decimal to String* | Convert a decimal value to a string for formatted output. | `SELECT CAST(123.45 AS VARCHAR(10));` | `'123.45'` |
| *Date to String* | Convert a date to a string format for display. | `SELECT CAST(CURRENT_DATE() AS VARCHAR(20));` | `'2024-10-22'` |
| *String to Floating Point* | Convert a string to a floating-point number for calculations. | `SELECT CAST('123.45' AS FLOAT);` | `123.45` |

What happens if the format doesn’t meet the requirements? For example, if you try to convert a random text into a temporal data type?

```sql
SELECT CAST('SQL Academy' AS DATETIME);
```

In some databases it will work without any issues and `NULL` will be returned. However, some database will return error.