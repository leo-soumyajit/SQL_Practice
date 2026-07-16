# SQL Practice Challenge

## Challenge 3: Employees Earning More Than Their Managers

**Concepts Covered:** `SELF JOIN`, `INNER JOIN`, Table Aliases.

### 1. Database Schema

#### **`Employee` Table**
| Column Name | Data Type | Constraints / Description |
| :--- | :--- | :--- |
| `id` | INT | PRIMARY KEY |
| `name` | VARCHAR(50) | Employee's name |
| `salary` | INT | Employee's salary |
| `manager_id` | INT | `id` of this employee's manager (NULL if they are the boss) |

---

### 2. The Problem Statement
Write a single SQL query to find the names of all employees who earn strictly **more than** their direct managers.

**Required Output Column:** `Employee_Name`

---

### 3. My Solution (Using Self Join)
```sql
SELECT 
    e.name AS Employee_Name
FROM Employee AS e
INNER JOIN Employee AS m 
    ON e.manager_id = m.id
WHERE e.salary > m.salary;