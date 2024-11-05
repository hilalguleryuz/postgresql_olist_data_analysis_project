## Case 1: Order Analysis

Question 1:
- Examine the monthly order distribution.

```sql
select
     (date_trunc('month', order_approved_at))::date as order_month,
     count(order_id) as order_count
from orders
where order_approved_at is not null
group by 1
order by 1;
```
