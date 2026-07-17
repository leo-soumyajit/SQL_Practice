# SQL Practice Challenge

## Challenge 6: Customers Who Visited but Did Not Transact

**Concepts Covered:** `LEFT JOIN`, `IS NULL` Filtering, `GROUP BY`, `COUNT`, Handling NULLs in Aggregation.

### 1. Database Schema

#### **`visits` Table**
| Column Name | Data Type | Constraints / Description |
| :--- | :--- | :--- |
| `visit_id` | INT | PRIMARY KEY. Unique ID for a visit. |
| `customer_id` | INT | ID of the visiting customer. |

#### **`transactions` Table**
| Column Name | Data Type | Constraints / Description |
| :--- | :--- | :--- |
| `transaction_id` | INT | PRIMARY KEY. |
| `visit_id` | INT | FOREIGN KEY referencing `visits` table. |
| `amount` | INT | Transaction amount. |

---

### 2. The Problem Statement
Write an SQL query to find the IDs of the customers who visited the platform but **did not make any transactions**, and calculate the number of times they made these "empty" visits.

**Required Output Columns:** `customer_id`, `count_no_trans`

#### **Sample Output:**
| customer_id | count_no_trans |
| :--- | :--- |
| 54 | 2 |
| 30 | 1 |
| 96 | 1 |

---

### 3. My Solution
```sql
SELECT 
    visits.customer_id,
    COUNT(visits.visit_id) AS count_no_trans
FROM visits 
LEFT JOIN transactions 
    ON visits.visit_id = transactions.visit_id
WHERE transactions.transaction_id IS NULL
GROUP BY visits.customer_id;