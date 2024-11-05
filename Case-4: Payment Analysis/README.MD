## Case 4: Payment Analysis

#### Question 1:
- In which region do users with a high number of installments when making payments live the most?

```sql
with payment_analysis as (
select
	customer_unique_id,
	payment_installments,
	customer_state
from payments p
left join orders o on p.order_id = o.order_id
left join customers c on o.customer_id = c.customer_id
where payment_installments > 3
)
select
	customer_state,
	count(distinct customer_unique_id) as customer_count
from payment_analysis
group by 1
order by 2 desc;
```
### EXCEL OUTPUT
<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-4%3A%20Payment%20Analysis/Case4/Case4-Q1-G.png" alt="alt text" width="750"/>

The above graph shows the regions where customers with more than 3 installments live the most. The relevant customers live mostly in the Sao Paulo region. Sao Paulo is one of the largest regions in Brazil. Therefore, the dense population in the region positively affects trade activities. In large regions like Sao Paulo, the population is higher, the economic situation is better and the habit of shopping online is higher. For these reasons, we expect both e-commerce to develop faster and the number of orders to be higher in Sao Paulo compared to other regions. At the same time, the good economic situation has caused the purchase of more expensive products and the payments made with a higher number of installments to be mostly from this region.
____
#### Question 2:
- Calculate the number of successful orders and total successful payment amount by payment type.

```sql
select
	payment_type,
	count(order_status) AS basarili_odeme_sayisi,
	sum(payment_value)::integer as basarili_odeme_tutari
from payments p
left join orders o ON p.order_id = o.order_id
where order_status = 'delivered’
group by 1
order by 2 desc;
```
### SQL OUTPUT
![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-4%3A%20Payment%20Analysis/Case4/Case4-Q2.png)

### EXCEL OUTPUT
<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-4%3A%20Payment%20Analysis/Case4/Case4-Q2-G.png" alt="alt text" width="750"/>

When we examine the graph above, we see that the most used payment method is credit card and the least used method is debit card.
____
#### Question 3:
- Perform category-based analysis of orders paid in one payment.

```sql
select
	category_name_english,
	count(distinct p.order_id) as order_count
from payments p
left join orders o on p.order_id = o.order_id
left join items i on o.order_id = i.order_id
left join products pr on i.product_id = pr.product_id
left join translation t on pr.product_category_name = t.category_name
where payment_installments = 1 and category_name_english is not null
group by 1
order by 2 desc;
```
### SQL OUTPUT
![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-4%3A%20Payment%20Analysis/Case4/Case4-Q3.png)

### EXCEL OUTPUT
<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-4%3A%20Payment%20Analysis/Case4/Case4-Q3-G.png" alt="alt text" width="750"/>

In the graph above, we see the total number of orders paid with a single payment, grouped by category. In this graph, I have shown the top 20 categories with the most orders. According to this result, products in the sports/entertainment category were purchased the most with a single payment. This category is followed by computer accessories and health/beauty categories.
____
#### Question 4:
- Perform a category-based analysis of orders paid in installments. In which categories is payment in installments used the most?

```sql
select
	category_name_english,
	count(distinct o.order_id) as order_count
from payments p
left join orders o on p.order_id = o.order_id
left join items i on o.order_id = i.order_id
left join products pr on i.product_id = pr.product_id
left join translation t on pr.product_category_name = t.category_name
where payment_installments > 1 and category_name_english is not null
group by 1
order by 2 desc;
```
### SQL OUTPUT
![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-4%3A%20Payment%20Analysis/Case4/Case4-Q4.png)

### EXCEL OUTPUT
<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-4%3A%20Payment%20Analysis/Case4/Case4-Q4-G.png" alt="alt text" width="750"/>

In the graph above, we see the total number of orders paid in installments grouped by category. In this graph, I have shown the top 20 categories with the most orders. According to this result, the bedroom and bathroom category products were purchased the most in installments. This category is followed by health/beauty and watch categories.











