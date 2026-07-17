## Challenge 5: Restaurant Order Status Pivot 

**Concepts Covered:** Conditional Aggregation (`SUM` with `CASE WHEN`), Pivoting Rows to Columns, `INNER JOIN`, `GROUP BY`.

### 1. Database Schema

#### **`restaurants` Table**
| Column Name | Data Type | Constraints |
| :--- | :--- | :--- |
| `id` | INT | PRIMARY KEY |
| `name` | VARCHAR(50) | Restaurant Name |

#### **`orders` Table**
| Column Name | Data Type | Constraints |
| :--- | :--- | :--- |
| `order_id` | INT | PRIMARY KEY |
| `restaurant_id` | INT | FOREIGN KEY |
| `status` | VARCHAR(20) | 'DELIVERED', 'CANCELLED', 'REFUNDED' |

---

### 2. The Problem Statement
Write an SQL query to pivot the order status data. Calculate the total number of orders in each status category ('DELIVERED', 'CANCELLED', and 'REFUNDED') for every restaurant, displaying them as separate columns in a single row per restaurant.

**Required Output Columns:** `name`, `total_orders`, `delivered_count`, `cancelled_count`, `refunded_count`

---

### 3. My Solution (Using Conditional Aggregation)
```sql
SELECT 
    restaurants.name,
    count(orders.status) AS total_orders,
    SUM(CASE WHEN orders.status = 'DELIVERED' THEN 1 ELSE 0 END) AS delivered_count,
    SUM(CASE WHEN orders.status = 'CANCELLED' THEN 1 ELSE 0 END) AS cancelled_count,
    SUM(CASE WHEN orders.status = 'REFUNDED' THEN 1 ELSE 0 END) AS refunded_count
FROM restaurants 
INNER JOIN orders 
    ON restaurants.id = orders.restaurant_id
GROUP BY restaurants.name;