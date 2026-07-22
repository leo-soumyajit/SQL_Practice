# User Activity for the Past 30 Days I

## Problem Statement
Write an SQL query to find the daily active user count for a period of 30 days ending `2019-07-27` inclusively. A user was active on a date if they made at least one activity on that day.

Return the result table with columns `day` and `active_users`.

**Table: Activity**
| Column Name   | Type    | Description |
| :---          | :---    | :---        |
| user_id       | int     | The ID of the user |
| session_id    | int     | The session ID |
| activity_date | date    | The date of the activity |
| activity_type | enum    | Type of activity |

*(Note: There is no primary key for this table, it may have duplicate rows.)*

---

## Solution

### Approach: Grouping and Distinct Counting
To find the daily active users within a specific time frame, we need to filter the dates, group the records by day, and count the unique users:
1. **Filtering:** We use the `WHERE` clause with the `BETWEEN` operator to restrict the data to the 30-day window ending on `2019-07-27` (i.e., from `2019-06-28` to `2019-07-27`).
2. **Grouping:** We use `GROUP BY activity_date` to aggregate the records so that we can calculate metrics on a per-day basis.
3. **Counting Unique Users:** We use `COUNT(DISTINCT user_id)` to ensure that even if a user performs multiple activities in a single day, they are only counted once towards that day's active user total.
4. **Aliasing:** We alias `activity_date` as `day` and the count result as `active_users` to match the expected output format.

### SQL Query
```sql
SELECT 
    activity_date AS day, 
    COUNT(DISTINCT user_id) AS active_users 
FROM Activity
WHERE activity_date BETWEEN DATE('2019-06-28') AND DATE('2019-07-27')
GROUP BY activity_date;