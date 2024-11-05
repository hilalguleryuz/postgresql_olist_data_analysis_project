## 🚀 Olist E-commerce Data Analysis Project

The Olist e-commerce dataset is a collection of data provided by Olist, a Brazilian online marketplace that allows small and medium-sized businesses to sell their products. The dataset includes information about customer orders, product details, payment methods, reviews, and seller data.

You can see the SQL diagram of the dataset below:

![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Olist_ERD_diagram.png)

## Case 1: Order Analysis
### Question 1:
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

![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q1.png)

### EXCEL CHART

<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q1-G.png" alt="alt text" width="750"/>

When we examine the output, we see a regular increase in the number of orders over the months. There is a significant increase especially in November 2017. The Black Friday implemented in November may have been effective in this increase. There is another significant increase in January 2018, the reason for this may be the salary increases made in the new year or the gifts received for the new year/Christmas celebrations.
______
### Question 2:
- Examine the order numbers in the monthly order status breakdown. Are there any months with a dramatic decrease or increase?

```sql
select
       (date_trunc('month', order_approved_at))::date as order_month,
       order_status,
       count(order_id) as order_count
from orders
where order_approved_at is not null
group by 1,2
order by 1;
```
### SQL OUTPUT

![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q2.png)

### EXCEL CHART

<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q2-G1.png" alt="alt text" width="750"/>

When we examine the graph, we see a regular increase in the number of delivered orders over the months. There is a sudden increase especially in November 2017, the reason for this may be the special campaigns made in the relevant month or the Black Friday implemented all over the world in November. Again, there is a dramatic increase in January 2018. The reason for this may be the salary increases made in the new year or the gifts received for New Year/Christmas celebrations. There is also a serious increase in March 2018. Women's Day (March 8), celebrated worldwide, may have been effective in this increase.
______
### Question 3:
- Examine the order numbers in the product category breakdown. What are the categories that stand out on special days? For example, New Year's, Valentine's Day, etc.

```sql
with special_days as (
select
     to_char(order_approved_at, 'MM-YYYY’) as order_date,
     category_name_english,
     count(distinct o.order_id) as order_count,
     row_number() over (partition by to_char(order_approved_at, 'MM-YYYY') order by count(distinct o.order_id) desc) as rn
from orders o
left join items i on o.order_id = i.order_id
left join products p on i.product_id = p.product_id
left join translation t on p.product_category_name = t.category_name
where
     to_char(order_approved_at, 'MM') = '02’ or --sevgililer günü için
     to_char(order_approved_at, 'MM') = '12' --yılbaşı/noel için
group by 1,2
)
select * from special_days where rn between 1 and 5;
```

### SQL OUTPUT

![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q3.png)

### EXCEL CHART

<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q3-G.png" alt="alt text" width="750"/>

In the chart above, the order numbers are grouped by category and include the months of Valentine's Day and New Year's/Christmas. I examined the 5 categories that stand out in the months of the relevant special days. For example, when we look at December 2017 for New Year's/Christmas, bedroom and bathroom products, sports, health/beauty, toys and watches are among the most ordered categories. The fact that the toy category is in the top 5 may be due to the gifts bought for children at Christmas. Again, the watch and health/beauty categories are among the gifts bought at New Year's and therefore are among the top 5 categories. Since our data does not include December 2016 and December 2018, we cannot make any comments about New Year's/Christmas for those periods. We see that the health/beauty category is one of the most ordered categories for Valentine's Day in February 2018.
______
### Question 4:
- Examine the order numbers based on days of the week and days of the month. Create a visual in Excel with the output of the query you wrote and interpret it.

For days of the week:
```sql
select
to_char(order_purchase_timestamp, 'Day’) as days_of_week,
count(order_id) as order_count
from orders
where order_purchase_timestamp is not null
group by 1
order by 2 desc;
```

### SQL OUTPUT

![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q4.png)

### EXCEL CHART

<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q4-G.png" alt="alt text" width="700"/>

The most shopping days are Monday, Tuesday and Wednesday, while the least shopping day is Saturday. When we examine people's shopping behavior, the tendency to shop is mostly from the beginning to the middle of the week. This tendency decreases towards the weekend. At the beginning of the week, people usually start planning and purchasing their weekly needs. In addition, stores usually start new discounts and campaigns at the beginning of the week. For this reason, we see an increased shopping tendency at the beginning of the week. Weekends are usually the days when people spend time for rest, family events and hobby activities. Therefore, the time and money spent on shopping may decrease.
____
For days of the month:
```sql
select
to_char(order_purchase_timestamp, 'DD’) as days_of_month,
count(order_id) as order_count
from orders
where order_purchase_timestamp is not null
group by 1
order by 1;
```

### SQL OUTPUT

![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q5.png)

### EXCEL CHART

<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Screenshots/Case1/Case1-Q5-G.png" alt="alt text" width="750"/>

According to the graph above, we see that the number of orders placed increases on the 24th of the month and the highest number of orders are reached in the month. Salaries may be deposited on the 24th of the month, which may cause a dramatic increase in the number of orders. On the 31st of the month, the lowest number of orders are made in the month.













