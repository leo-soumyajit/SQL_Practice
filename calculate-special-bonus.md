# Calculate Special Bonus

## Problem Statement
Write an SQL query to calculate the bonus of each employee. The bonus of an employee is `100%` of their salary if the `employee_id` is an **odd number** and the employee's `name` does **not start with the character 'M'**. The bonus of an employee is `0` otherwise.

Return the result table ordered by `employee_id`.

**Table: Employees**
| Column Name | Type    | Description |
| :---        | :---    | :---        |
| employee_id | int     | Primary Key |
| name        | varchar | Employee Name|
| salary      | int     | Employee Salary|

---

## Solution

### Approach: Conditional Logic using `CASE`
We can solve this by applying a conditional `CASE` statement inside the `SELECT` clause. We need to check two conditions:
1. `employee_id % 2 != 0` (To ensure the ID is odd).
2. `name NOT LIKE 'M%'` (To ensure the name does not start with the letter 'M').
If both conditions are met, the bonus is equal to the salary. Otherwise, it is an integer `0`. Finally, the results are sorted in ascending order of `employee_id`.

### SQL Query
```sql
SELECT 
    employee_id,
    CASE
        WHEN (employee_id % 2 != 0) AND name NOT LIKE 'M%' THEN salary
        ELSE 0
    END AS bonus
FROM Employees 
ORDER BY employee_id ASC;