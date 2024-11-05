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
![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-1%3A%20Order%20Analysis/Case1/Case1-Q1.png)

### EXCEL OUTPUT
<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-1%3A%20Order%20Analysis/Case1/Case1-Q1-G.png" alt="alt text" width="750"/>

When we examine the output, we see a regular increase in the number of orders over the months. There is a significant increase especially in November 2017. The Black Friday implemented in November may have been effective in this increase. There is another significant increase in January 2018, the reason for this may be the salary increases made in the new year or the gifts received for the new year/Christmas celebrations.
