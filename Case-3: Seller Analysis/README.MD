## Case 3: Seller Analysis

- Which sellers sell products from more categories? Do sellers with more categories also have more orders?

```sql
select
	s.seller_id,
	count(distinct product_category_name) category_count,
	count(distinct order_id) order_count
from sellers s
left join items i on s.seller_id = i.seller_id
left join products p on i.product_id = p.product_id
group by 1
having count(distinct product_category_name) > 10
order by 2 desc;
```
### SQL OUTPUT
![alt text](https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-3%3A%20Seller%20Analysis/Case3/Case3-Q1.png)

### EXCEL OUTPUT
<img src="https://github.com/hilalguleryuz/postgresql_olist_data_analysis_project/blob/main/Case-3%3A%20Seller%20Analysis/Case3/Case3-Q1-G.png" alt="alt text" width="750"/>

In the graph above, the category numbers and total order numbers of sellers who have made sales from more than 10 categories are given together. Since the query resulted in 40 different sellers, I numbered the sellers from 1 to 40 in order. I listed the number of categories the sellers made sales in from largest to smallest. In the same graph, I also showed the total number of orders received by the sellers. When we examine the graph, although seller number 3 has the highest number of orders, it does not have the highest number of categories. Again, when we look at seller number 35, although it has the second highest number of orders, it has made sales from only 11 categories. When we examine seller number 1, we see that it is the seller with the highest number of categories. However, the number of orders is quite low compared to other sellers. As a result, the number of orders of sellers with more categories is not high, and there is no relationship between the number of categories and the number of orders.
