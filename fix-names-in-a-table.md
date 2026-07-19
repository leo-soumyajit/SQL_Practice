# Fix Names in a Table

## Problem Statement
Write an SQL query to fix the names so that only the first character is uppercase and the rest are lowercase.

Return the result table ordered by `user_id`.

**Table: Users**
| Column Name | Type    | Description |
| :---        | :---    | :---        |
| user_id     | int     | Primary Key |
| name        | varchar | Employee Name|

---

## Solution

### Approach: String Manipulation
To format the names correctly, we use a combination of SQL string functions:
1. `LEFT(name, 1)` extracts the first character, and `UPPER()` capitalizes it.
2. `SUBSTRING(name, 2)` extracts the rest of the string starting from the second character, and `LOWER()` converts it to lowercase.
3. `CONCAT()` joins these two formatted parts together.
Finally, we alias this constructed string as `name` to match the expected output format and sort the results using `ORDER BY user_id ASC`.

### SQL Query
```sql
SELECT 
    user_id,
    CONCAT(UPPER(LEFT(name, 1)), LOWER(SUBSTRING(name, 2))) AS name
FROM Users 
ORDER BY user_id ASC;