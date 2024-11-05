## Case 2: Customer Analysis

- In which cities do customers shop more?

```sql
select
  customer_city,
  count(customer_unique_id)
from customers
group by 1
order by 2 desc;
```
### SQL OUTPUT
![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-2%3A%20Customer%20Analysis/Case2/Case2-Q1.png)

### EXCEL OUTPUT
<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-2%3A%20Customer%20Analysis/Case2/Case2-Q1-G.png" alt="alt text" width="750"/>

The top 20 cities where most shopping was done are shown in the chart above. The city where most shopping was done was Sao Paulo with 15.540 orders.
