SQL data analysis questions that can help you gain valuable insights to maximize the business of a music store:

## Sales Analysis:

### 1. What are the top 5 best-selling albums of all time -

```sql
SELECT TOP 5 a.album_id, a.title, SUM(il.quantity) AS total_sales
FROM album$ AS a
JOIN track$ AS t ON a.album_id = t.album_id
JOIN invoice_line$ AS il ON t.track_id = il.track_id
GROUP BY a.album_id, a.title
ORDER BY total_sales DESC
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 2. Which artists have generated the highest revenue from album sales -

```SQL
SELECT ar.artist_id, ar.name, SUM(il.unit_price * il.quantity) AS total_sales
FROM artist$ AS aR
JOIN album$ AS al ON ar.artist_id = al.artist_id
JOIN track$ AS t ON al.album_id = t.album_id
JOIN invoice_line$ AS il ON t.track_id = il.track_id
GROUP BY ar.artist_id, ar.name
ORDER BY total_revenue DESC;
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 3. Which media type has the highest sales volume and revenue -

```sql

SELECT mt.media_type_id,mt.name, SUM(il.quantity) as sales_volume, SUM(il.unit_price * il.quantity) AS total_revenue
FROM media_type$ AS mt
JOIN track$ AS t ON mt.media_type_id = t.media_type_id
JOIN invoice_line$ AS il ON t.track_id = il.track_id
GROUP BY mt.media_type_id,mt.name
ORDER BY total_revenue DESC;

```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 4. What is the average total sales per month for the past years?

```SQL

SELECT YEAR(invoice_date) AS [year], MONTH(invoice_date) AS [month], AVG(total) AS average_sales
FROM invoice$
WHERE invoice_date >= '2017-01-03' AND invoice_date <= '2020-12-30'
GROUP BY YEAR(invoice_date), MONTH(invoice_date)
ORDER BY YEAR(invoice_date), average_sales desc
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 5. How do sales vary by genre? Which genre has the highest sales revenue?

```SQL

SELECT g.name, SUM(il.unit_price * il.quantity) AS total_revenue
FROM genre$ g
JOIN track$ AS t ON g.genre_id = t.genre_id
JOIN invoice_line$ AS il ON t.track_id = il.track_id
GROUP BY g.name
ORDER BY total_revenue DESC;
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Customer Analysis:

### 1. Who are the top 10 highest-spending customers-
```SQL

SELECT c.customer_id, c.first_name + ' ' + c.last_name as Customer_name, SUM(i.total) AS total_spending
FROM customer$ AS c
JOIN invoice$ AS i ON c.customer_id = i.customer_id
GROUP BY c.customer_id, c.first_name, c.last_name
ORDER BY total_spending DESC
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 2. How many customers have made repeat purchases -

```SQL

SELECT COUNT(*) AS repeat_customers
FROM (
    SELECT customer_id
    FROM invoice$ 
    GROUP BY customer_id
    HAVING COUNT(DISTINCT invoice_id) > 1
) AS repeat_purchase_customers;
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 3. What is the average number of purchases per customer -

```SQL
SELECT AVG(purchase_count) AS average_purchases_per_customer
FROM (
    SELECT customer_id, COUNT(DISTINCT invoice_id) AS purchase_count
    FROM invoice$
    GROUP BY customer_id
) AS customer_purchases;
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 4. Which countries have the highest number of customers -
```SQL
SELECT country, COUNT(*) AS customer_count
FROM customer$
GROUP BY country
ORDER BY customer_count DESC
```
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 1.  What are the top-selling genres in terms of revenue?

```sql
SELECT g.name, SUM(il.unit_price * il.quantity) AS total_revenue
FROM genre$ g
JOIN track$  t ON g.genre_id = t.genre_id
JOIN invoice_line$ il  ON il.track_id = t.track_id
GROUP BY g.name
ORDER BY total_revenue desc
```
### 2. Which artists or genres that have shown significant growth in sales over time -

```sql
SELECT 
  ar.name AS artist_name,
  g.name AS genre_name,
  MIN(i.invoice_date) AS first_purchase_date,
  MAX(i.invoice_date) AS latest_purchase_date,
  SUM(il.quantity) AS total_sales_quantity
FROM invoice$ AS i
JOIN  invoice_line$ AS il ON i.invoice_id = il.invoice_id
JOIN  track$ AS t ON il.track_id = t.track_id
JOIN  album$ AS al ON t.album_id = al.album_id
JOIN  artist$ AS ar ON al.artist_id = ar.artist_id
JOIN  genre$ AS g ON t.genre_id = g.genre_id
GROUP BY  ar.name, g.name
ORDER BY  total_sales_quantity DESC;
```

## Top Selling Tracks and Albums:

### 1. What are the top-selling tracks of all time -
```sql
SELECT TOP 5 t.name,t.track_id, SUM(il.quantity) AS total_sales
from track$ AS t
JOIN invoice_line$ AS il ON t.track_id = il.track_id
GROUP BY t.name,t.track_id
ORDER BY total_sales DESC
```

### 2. Which albums have generated the highest revenue?
```sql

SELECT al.title,SUM(il.unit_price * il.quantity) AS total_revenue
from album$ AS al 
JOIN track$ AS t ON al.album_id = t.album_id
JOIN invoice_line$ AS il ON t.track_id = il.track_id
GROUP BY al.title
ORDER BY total_revenue DESC;
```
### 3. What is the distribution of customers by geographic location?

```sql
select country , state,city,count(*) from customer$
group by country , state,city
```

### 4. What are the peak sales periods during the year?
```sql
SELECT
  DATEPART(YEAR, invoice_date) AS year,
  DATEPART(MONTH, invoice_date) AS month,
  SUM(total) AS total_sales
FROM invoice$
GROUP BY DATEPART(YEAR, invoice_date), DATEPART(MONTH, invoice_date)
ORDER BY  SUM(total) DESC;
```
### 5.Which employees have the highest sales volume?

```sql
SELECT 
    e.employee_id,
    e.first_name,
    e.last_name,
    SUM(i.total) AS total_sales
FROM 
    employee$ e
JOIN 
    customer$ c ON e.employee_id = c.support_rep_id
JOIN 
    invoice$ i ON c.customer_id = i.customer_id
GROUP BY 
    e.employee_id,
    e.first_name,
    e.last_name
ORDER BY 
    total_sales DESC;
```

