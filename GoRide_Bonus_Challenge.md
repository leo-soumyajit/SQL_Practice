---

## Challenge 4: The "GoRide" Driver Bonus Campaign

**Concepts Covered:** `CASE WHEN` (Conditional Logic), `INNER JOIN`, `GROUP BY`, `HAVING`, Aggregation (`ROUND`, `AVG`, `COUNT`).

### 1. Database Schema

#### **`drivers` Table**
| Column Name | Data Type | Constraints |
| :--- | :--- | :--- |
| `driver_id` | INT | PRIMARY KEY |
| `name` | VARCHAR(50) | Driver's Name |

#### **`rides` Table**
| Column Name | Data Type | Constraints |
| :--- | :--- | :--- |
| `ride_id` | INT | PRIMARY KEY |
| `driver_id` | INT | FOREIGN KEY |
| `status` | VARCHAR(20) | Values: 'COMPLETED', 'CANCELLED' |
| `rating` | DECIMAL(3,1) | Ride rating (e.g., 4.5, 3.8) |

---

### 2. The Problem Statement
Write a single SQL query to generate a Driver Bonus Report based on the following rules:
1. Only drivers who have strictly **more than 2 'COMPLETED' rides** are eligible.
2. If average rating is **>= 4.5**, bonus is **'$50'**.
3. If average rating is **between 4.0 and 4.4**, bonus is **'$20'**.
4. Otherwise, bonus is **'$0'**.

**Required Output Columns:** `driver_name`, `count(status)`, `avg_rating`, `bonus_amount`

---

### 3. My Solution
```sql
SELECT 
    drivers.name,
    count(status),
    round(avg(rating),1) as avg_rating,
    case
        when round(avg(rating),1) >= 4.5 then '$50'
        when round(avg(rating),1) between 4.0 and 4.4 then '$20'
        else '$0'
    end as bonus_amount
FROM drivers
INNER JOIN rides
    ON drivers.driver_id = rides.driver_id
WHERE status = 'COMPLETED'
GROUP BY drivers.name
HAVING count(status) > 2;