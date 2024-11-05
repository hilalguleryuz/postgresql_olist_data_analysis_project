## 🚀 Olist E-commerce Data Analysis Project

The Olist e-commerce dataset is a collection of data provided by Olist, a Brazilian online marketplace that allows small and medium-sized businesses to sell their products. The dataset includes information about customer orders, product details, payment methods, reviews, and seller data.

You can see the SQL diagram of the dataset below:

![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Olist_ERD_diagram.png)

### Case 1: Order Analysis
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
![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q1.png)

![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q1-G.png)

When we examine the output, we see a regular increase in the number of orders over the months. There is a significant increase especially in November 2017. The Black Friday implemented in November may have been effective in this increase. There is another significant increase in January 2018, the reason for this may be the salary increases made in the new year or the gifts received for the new year/Christmas celebrations.
