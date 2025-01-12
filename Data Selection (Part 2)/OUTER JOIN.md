# OUTER JOIN 🌍✨

An _OUTER JOIN_ is used to retrieve rows from two tables, including the matched rows and unmatched rows from one or both tables.

<aside>

💡 OUTER JOIN is useful when you want to ensure no data is left behind, even if there are no matching rows in the other table.

</aside>

🔍 How It Works:
- 🔗 The OUTER JOIN compares the columns specified in the _ON_ clause
- ✅ Rows with matching values in both tables are included.
- ❓ Rows without a match in one table are still included, with _NULL_ values for the missing columns.


# Types of OUTER JOINs
- `LEFT OUTER JOIN:` 🖼️ 
    - Includes all rows from the left table, along with matched rows from the right table. If there is no match, the right-side columns will have _NULL_ values.
- `RIGHT OUTER JOIN:` ➡️
    - Includes all rows from the right table, along with matched rows from the left table. If there is no match, the left-side columns will have _NULL_ values.
- `FULL OUTER JOIN:` 🌐
    - Includes all rows from both tables. If a row has no match in one table, the columns from that table will contain _NULL_ values.


# When to Use OUTER JOIN 🛠️
- 🧐 To identify missing or unmatched data between tables.
- 📊 For creating complete reports where no information is excluded, even if some relationships are incomplete.

<aside>

💡 Tip: Always think about whether you need unmatched data. If you do, an _OUTER JOIN_ ensures that no rows are lost!

</aside>