# Managers with at Least 5 Direct Reports

## Problem Statement
Write an SQL query to report the managers with at least **five direct reports**.

Return the result table in any order.

**Table: Employee**
| Column Name | Type | Description |
| :--- | :--- | :--- |
| id | int | Primary Key for this table. |
| name | varchar | The name of the employee. |
| department | varchar | The department of the employee. |
| managerId | int | The ID of the employee's manager. (Can be NULL) |

---

## Solution

### Approach: Self-Join and Aggregation
To find managers with 5 or more direct reports, we can treat the `Employee` table as two distinct entities: an "Employees" table and a "Managers" table.
1. **Self-Join:** We perform an `INNER JOIN` of the `Employee` table to itself. We use the alias `e` for the employees (the ones reporting) and `ee` for the managers. The join condition is `e.managerId = ee.id`.
2. **Grouping:** We group the joined results by the manager's identifier (`ee.id` or `ee.name`) to aggregate all the employees reporting to each specific manager.
3. **Filtering Aggregates:** We use the `HAVING` clause, which allows us to filter based on aggregated data. We check if the count of reports (`COUNT(e.managerId)`) is greater than or equal to 5.
4. **Selection:** Finally, we select the manager's name (`ee.name`).

### SQL Query
```sql
SELECT 
    ee.name 
FROM Employee e
INNER JOIN Employee ee 
    ON e.managerId = ee.id
GROUP BY ee.name
HAVING COUNT(e.managerId) >= 5;