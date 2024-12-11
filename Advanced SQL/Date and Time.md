# Date and Time 📅

SQL provides robust support for handling *date and time* data through various data types and functions. Date and time are crucial for tracking records, performing time-based calculations and scheduling events in databases.

Dealing with date and time format might be really tricky sometimes because:

- Various formats for representing dates and times
- The presence of time zones
- The non-obvious calculations involving temporal data, such as determining age

# Date and Time Data Types 📅

| **Data Type** | **Description** | **Format** | **Use Cases** |
| --- | --- | --- | --- |
| `DATE` | Stores date values (year, month, day) | `YYYY-MM-DD` | Birthdates, event dates |
| `TIME` | Stores time values (hours, minutes, seconds) | `HH:MM:SS` | Scheduling, time tracking |
| `DATETIME` | Stores both date and time | `YYYY-MM-DD HH:MM:SS` | Timestamps for records, logging |
| `TIMESTAMP` | Stores date and time with UTC tracking | `YYYY-MM-DD HH:MM:SS` | Record creation/update times |
| `INTERVAL` | Represents a period of time | `n unit` (e.g., `5 DAY`) | Date/time arithmetic (adding/subtracting) |

Let’s generate some examples:

```sql
SELECT
    CAST("2022-06-16 16:37:23" AS DATETIME) AS datetime_1,
    CAST("2014/02/22 16*37*22" AS DATETIME) AS datetime_2,
    CAST("20220616163723" AS DATETIME) AS datetime_3,
    CAST("2021-02-12" AS DATE) AS date_1,
    CAST("160:23:13" AS TIME) AS time_1,
    CAST("89" AS YEAR) AS year;
```

In the above query, the `CAST` function was used to explicitly convert a string into a *date* and *time*. This is necessary when the server doesn’t expect a temporal value and therefore doesn’t automatically convert the string to the appropriate type.

# Date and Time Functions 📐

Here’s a summary table of *Common Date and Time Functions* in SQL:

| **Function** | **Description** | **Example** | **Result** |
| --- | --- | --- | --- |
| `CURRENT_DATE()` | Returns the current date | `SELECT CURRENT_DATE();` | `2024-10-22` |
| `CURRENT_TIME()` | Returns the current time | `SELECT CURRENT_TIME();` | `14:30:00` |
| `NOW()` | Returns the current date and time | `SELECT NOW();` | `2024-10-22 14:30:00` |
| `EXTRACT(*field* FROM *date*)` | Extracts a specific part of a date (e.g., year, month) | `SELECT EXTRACT(YEAR FROM '2024-10-22');` | `2024` |
| `DATE_ADD(*date*, INTERVAL expr unit)` | Adds a specified interval to a date | `SELECT DATE_ADD('2024-10-22', INTERVAL 5 DAY);` | `2024-10-27` |
| `DATE_SUB(*date*, INTERVAL expr unit)` | Subtracts a specified interval from a date | `SELECT DATE_SUB('2024-10-22', INTERVAL 10 DAY);` | `2024-10-12` |
| `DATEDIFF(*date1*, *date2*)` | Returns the difference in days between two dates | `SELECT DATEDIFF('2024-10-22', '2024-10-01');` | `21` |
| `STR_TO_DATE(*str*, *format*)` | Converts a string into a date using a specified format | `SELECT STR_TO_DATE('22-10-2024', '%d-%m-%Y');` | `2024-10-22` |
| `DATE_FORMAT(*date*, *format)*` | Formats a date according to a specified format | `SELECT DATE_FORMAT('2024-10-22', '%W, %M %d, %Y');` | `Tuesday, October 22, 2024` |

# Time Zones 🕒

Since people around the world want noon to roughly correspond to the sun's highest point, there has never been a task to use universal time, and the world has been divided into 24 time zones.

*UTC (Coordinated Universal Time)* serves as the reference point. All other time zones can be described by the number of hours offset from *UTC*. For example, Moscow's time zone can be described as *UTC+3*.

The time zone is one of the database server settings and can be set:

- Globally
- For the current user
- For the current user session

```sql
SET GLOBAL time_zone = '+03:00';    // globally
SET time_zone = '+03:00';           // for the current user
SET @@session.time_zone = '+03:00'; // for the current user session
```

The problem with this approach is that it doesn’t account for whether the person's birthday has already occurred this year. If July 3rd has passed, the person has celebrated their birthday and is now 20 years old; otherwise, they are still 19. The difference in the `YEAR` function would be misleading, as it would yield 20 in both cases.

If calculating age by year difference isn’t effective, one might consider finding the age through the difference in days between two dates and then dividing that difference by the number of days in a year, rounding down:

```sql
SELECT FLOOR(DATEDIFF(NOW(), '2003-07-03 14:10:26') / 365);
```

This solution would be much more accurate than the previous one. However, it still wouldn't be completely precise due to leap years, where a year has 366 days. While the margin of error for one person's age due to leap years is relatively low, this error can accumulate when calculating the average age among a specific group of people and distort the actual values.

So, how can we accurately determine age? For this, there is a built-in function — `TIMESTAMPDIFF` 

It takes the unit of measurement as the first argument and returns the difference between two temporal values:

```sql
SELECT TIMESTAMPDIFF(YEAR, '2003-07-03 14:10:26', NOW());
```

# How to Choose Right Time Data Type? **🤔**

- ***Precision:***
    - Choose `DATETIME` or `TIMESTAMP` if you need both date and time. If only one is needed, use `DATE` or `TIME`.
- ***Time Zone:***
    - If time zone management is important, consider using `TIMESTAMP` since it often includes time zone information, making it suitable for applications with global users.
- ***Storage Requirements:***
    - Different data types may consume different amounts of storage space. Be aware of these differences when designing your database schema.
- ***Compatibility:***
    - Check your SQL database documentation, as date and time formats can vary between systems (e.g., MySQL, PostgreSQL)