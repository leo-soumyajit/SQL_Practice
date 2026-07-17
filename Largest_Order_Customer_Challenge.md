# SQL Practice Challenge

## Challenge 8: Customer Placing the Largest Number of Orders

**Concepts Covered:** `GROUP BY`, `ORDER BY ... DESC`, `LIMIT`, and SQL Clause Execution Order.

### 1. Database Schema

#### **`orders` Table**
| Column Name | Data Type | Constraints / Description |
| :--- | :--- | :--- |
| `order_number` | INT | PRIMARY KEY. |
| `customer_number` | INT | ID of the customer who placed the order. |

---

### 2. The Problem Statement
Write an SQL query to find the `customer_number` for the customer who has placed the **largest number of orders**.
*(Assume that exactly one customer will have placed more orders than any other customer).*

**Required Output Column:** `customer_number`

#### **Sample Output:**
| customer_number |
| :--- |
| 3 |

---

### 3. My Solution
```sql
SELECT customer_number
FROM orders
GROUP BY customer_number
ORDER BY COUNT(order_number) DESC
LIMIT 1;
```

---

### 4. 💡 Key Takeaways & Interview Notes
* **Strict SQL Order of Clauses:** `SELECT` -> `FROM` -> `WHERE` -> `GROUP BY` -> `HAVING` -> `ORDER BY` -> `LIMIT`. 
* **`LIMIT` Placement:** `LIMIT` must always be the very last clause in your query. 
* **`ORDER BY` with Aggregation:** You can sort your results using an aggregate function (like `COUNT()`) directly in the `ORDER BY` clause, even if you don't display that count in the `SELECT` clause.