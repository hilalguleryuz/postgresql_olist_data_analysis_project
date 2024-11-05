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

### SQL OUTPUT
![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-1%3A%20Order%20Analysis/Case1/Case1-Q1.png)

### EXCEL OUTPUT
<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-1%3A%20Order%20Analysis/Case1/Case1-Q1-G.png" alt="alt text" width="750"/>
