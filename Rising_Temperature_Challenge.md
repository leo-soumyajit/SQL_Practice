# SQL Practice Challenge

## Challenge 7: Rising Temperature

**Concepts Covered:** `SELF JOIN`, Date Functions (`DATEDIFF`), Comparing rows within the same table.

### 1. Database Schema

#### **`weather` Table**
| Column Name | Data Type | Constraints / Description |
| :--- | :--- | :--- |
| `id` | INT | PRIMARY KEY. |
| `record_date` | DATE | The date of the weather record. |
| `temperature` | INT | The temperature recorded on that day. |

---

### 2. The Problem Statement
Write an SQL query to find all dates' `id` with higher temperatures compared to its previous dates (yesterday).

**Required Output Column:** `id`

#### **Sample Output:**
| id |
| :--- |
| 2 |
| 4 |

---

### 3. My Solution (Using SELF JOIN and DATEDIFF)
```sql
SELECT 
    w1.id 
FROM weather AS w1 
INNER JOIN weather AS w2
    ON DATEDIFF(w1.record_date, w2.record_date) = 1
WHERE w1.temperature > w2.temperature;