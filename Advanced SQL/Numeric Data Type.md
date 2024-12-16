# Numeric Data Type  🔢

<aside>

📖**Numeric Data Type** — numerical values (integers or decimals).

</aside>

These types are essential when dealing with any kind of numerical data such as *IDs*, *prices*, *quantities* or *measurements*. The choice of numeric data type affects both the accuracy of the values and the amount of storage required. When performing calculations, all standard arithmetic operations: `+,  -,  *,  /, ...` can be used and the order of operations can be modified using parentheses.

```sql
SELECT 12 * ((4 - 16) / (2 + 1)) AS calc_example;
```

Here’s a table summarizing the *Numeric Data Types* in SQL:

| **Data Type** | **Description** | **Range** | **Storage Size** | **Use Cases** |
| --- | --- | --- | --- | --- |
| `INT` | Standard integer type for whole numbers | `-2,147,483,648` to `2,147,483,647` | 4 bytes | General whole numbers (e.g., IDs, counts) |
| `SMALLINT` | Smaller integer type for whole numbers | `-32,768` to `32,767` | 2 bytes | Small whole numbers (e.g., age, ranks) |
| `BIGINT` | Large integer type for bigger numbers | `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807` | 8 bytes | Very large numbers (e.g., population) |
| `DECIMAL(p, s)` | Exact fixed-point numbers with precision `p` and scale `s` | Defined by precision and scale | Varies based on precision | Financial data (e.g., prices, currency) |
| `FLOAT` | Approximate floating-point number | Varies depending on the database implementation | 4 bytes or 8 bytes (depending on precision) | Scientific calculations |
| `REAL` | Smaller precision floating-point number | Varies depending on the database implementation | 4 bytes | Less precise calculations |

# How to Choose Right Numeric Data Type? **🤔**

When selecting a numeric data type, consider the following factors:

- ***Range of Values:***
    - Choose a type that can accommodate the maximum and minimum values you expect to store. For instance, if you need to store age, a `TINYINT` may suffice, but for larger values like population counts, `BIGINT` would be more appropriate.
- ***Precision:***
    - For financial applications where accuracy is critical (e.g., currency calculations), use `DECIMAL` or `NUMERIC`. These types prevent rounding errors inherent in floating-point arithmetic.
- ***Storage Efficiency:***
    - Smaller numeric types (like `TINYINT` or `SMALLINT`) save space in your database. If storage is a concern, choose the smallest data type that meets your needs.
- ***Performance:***
    - While the performance difference between numeric types is often negligible, smaller types may lead to better performance in large datasets due to reduced I/O and improved cache efficiency.

# Mathematical Functions in SQL 🧮

SQL provides various *mathematical functions* to perform calculations and manipulate numeric data. These functions are useful when working with data that requires arithmetic operations, statistical analysis, or other forms of numeric transformation.

Here’s a table summarizing common *Mathematical Functions* in SQL:

| **Function** | **Description** | **Example** | **Result** |
| --- | --- | --- | --- |
| `ABS(x)` | Returns the absolute (non-negative) value of `x` | `SELECT ABS(-15);` | 15 |
| `CEIL(x)` | Rounds `x` up to the nearest integer | `SELECT CEIL(4.2);` | 5 |
| `FLOOR(x)` | Rounds `x` down to the nearest integer | `SELECT FLOOR(4.9);` | 4 |
| `ROUND(x, d)` | Rounds `x` to `d` decimal places | `SELECT ROUND(3.14159, 2);` | 3.14 |
| `POWER(x, y)` | Returns `x` raised to the power of `y` | `SELECT POWER(2, 3);` | 8 |
| `SQRT(x)` | Returns the square root of `x` | `SELECT SQRT(16);` | 4 |
| `MOD(x, y)` | Returns the remainder of `x` divided by `y` | `SELECT MOD(10, 3);` | 1 |
| `EXP(x)` | Returns `e` raised to the power of `x` | `SELECT EXP(1);` | 2.718281828 |
| `LOG(x)` | Returns the natural logarithm of `x` | `SELECT LOG(2.71828);` | 1 |
| `TRUNC(x, d)` | Truncates `x` to `d` decimal places without rounding | `SELECT TRUNC(4.567, 2);` | 4.56 |