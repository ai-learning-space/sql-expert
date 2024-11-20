# String Data Type 🆎

The *string* data type is the most commonly used data type in SQL. It allows for the storage of both *textual* and various *binary data* (such as images) within a database.

The string data type is represented by the following types:

| **Data Type** | **Description** | **Length** | **Use Case** |
| --- | --- | --- | --- |
| `CHAR(*n*)` | Fixed-length character string | n characters | Consistent-length data |
| `VARCHAR(*n*)` | Variable-length character string with a maximum length | Up to n characters | Names, addresses, variable-length data |
| `TEXT` | Variable-length string with no maximum limit | Unlimited | Large text fields, comments |
| `JSON` | Stores JSON data as text, preserving formatting | Unlimited | Semi-structured data |
| `JSONB` | Binary representation of JSON, optimized for storage | Unlimited | Efficient querying of JSON data |
| `BINARY(*n*)` | Fixed-length binary data | n bytes | Fixed-size binary data |
| `VARBINARY(*n*)` | Variable-length binary data with a maximum length | Up to n bytes | Images, variable-sized files |

# Choosing the Right String and Binary Data Type

- Use `CHAR` when you know the exact length of the data and want to enforce that length.
- Use `VARCHAR` for data where the length can vary but should not exceed a certain limit.
- Use `TEXT` for large amounts of text data or when length is unpredictable.
- Use `BINARY` for fixed-length binary data.
- Use `VARBINARY` for variable-length binary data.
- Consider `JSONB` when dealing with semi-structured data that may need to be queried efficiently.