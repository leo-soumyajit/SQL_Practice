# SQL Practice Challenge

## Challenge 9: Duplicate Emails

**Concepts Covered:** `GROUP BY`, `HAVING` clause for filtering aggregations.

### 1. Database Schema

#### **`person` Table**
| Column Name | Data Type | Constraints / Description |
| :--- | :--- | :--- |
| `id` | INT | PRIMARY KEY. |
| `email` | VARCHAR | The email address of the person. |

---

### 2. The Problem Statement
Write an SQL query to report all the duplicate emails. 
*(A duplicate email is defined as an email that appears more than once in the table).*

**Required Output Column:** `Email`

#### **Sample Output:**
| Email |
| :--- |
| a@b.com |

---

### 3. My Solution
```sql
SELECT email
FROM person
GROUP BY email
HAVING COUNT(id) > 1;
```

---

### 4. 💡 Key Takeaways & Interview Notes
* **`WHERE` vs `HAVING`:** You cannot use aggregate functions like `COUNT()` inside a `WHERE` clause. `WHERE` filters rows *before* grouping. To filter *after* grouping based on an aggregate condition, you must use the `HAVING` clause.
* **Invisible Aggregation:** You can evaluate an aggregate function like `COUNT(id)` inside the `HAVING` clause without needing to display it in the `SELECT` clause. Service-based company coding platforms are strict about output columns, so only `SELECT` exactly what is asked.