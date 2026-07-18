# SQL Practice Challenge

## Challenge 10: Second Highest Salary

**Concepts Covered:** Subqueries, Aggregate Functions (`MAX`), Handling `NULL` values implicitly.

### 1. Database Schema

#### **`employee` Table**
| Column Name | Data Type | Constraints / Description |
| :--- | :--- | :--- |
| `id` | INT | PRIMARY KEY. |
| `salary` | INT | The salary of the employee. |

---

### 2. The Problem Statement
Write an SQL query to report the second highest distinct salary from the `employee` table. If there is no second highest salary, the query should report `NULL`.

**Required Output Column:** `SecondHighestSalary`

#### **Sample Output (Standard Case):**
| SecondHighestSalary |
| :--- |
| 65000 |

#### **Sample Output (Edge Case - Single Row / No 2nd Highest):**
| SecondHighestSalary |
| :--- |
| null |

---

### 3. My Solution
```sql
SELECT max(salary) AS SecondHighestSalary 
FROM employee
WHERE salary < (SELECT max(salary) FROM employee);