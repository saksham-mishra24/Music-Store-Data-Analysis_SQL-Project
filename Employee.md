### Command to see all tables in Databases -

```sql

SELECT name FROM sys.tables;
```
### 1. Who is the senior most employee based on job title -
```sql
SELECT  Top 1 * FROM employee$ 
ORDER BY hire_date ASC
```
### 2. Which countries have the most Invoices -
```sql
SELECT TOP 1 COUNT(invoice_id) as Invoices, billing_country
FROM invoice$
GROUP BY billing_country
ORDER BY Invoices desc
```



### 3. What are top 3 values of total invoice -
```sql
SELECT TOP 3 total
FROM invoice$
ORDER BY  total DESC
```

### 4. Who is the best customer - 
[ The customer who has spent the most money will be declared the best customer]
```sql
SELECT customer_id,SUM(total) as SPEND
FROM invoice$
GROUP BY customer_id
order by SPEND desc
```
### 5. Write a query that returns one city that has the highest sum of invoice totals -

[Return both the city name & sum of all invoice totals ]
```sql
SELECT billing_city, SUM(total) as revenue 
FROM invoice$
GROUP BY billing_city
ORDER BY revenue desc
```
### 6. Which city has the best customers -
[ We would like to throw a promotional Music Festival in the city we made the most money. ]

```SQL
SELECT TOP 5  a.customer_id, a.first_name  +  ' '  +  a.last_name as Customer_name, b.billing_city, SUM(b.total) as Revenue
FROM customer$ a
JOIN  invoice$ b
ON a.customer_id=b.customer_id
GROUP BY b.billing_city, a.customer_id, a.first_name, a.last_name
ORDER BY Revenue DESC
```


### 7. What are the top-selling genres in terms of revenue - 
```SQL

SELECT a.name, SUM(c.unit_price * c.quantity) AS Revenue
FROM genre$ a
JOIN track$ b ON a.genre_id = b.genre_id
JOIN invoice_line$ c ON b.track_id = c.track_id
GROUP BY a.name
ORDER BY Revenue DESC
```

### 8. Write query to return the email, first name, last name, & Genre of all Rock Music listeners -

```SQL
SELECT DISTINCT email,first_name, last_name
FROM customer$ c
JOIN invoice$ i ON c.customer_id = i.customer_id
JOIN invoice_line$ il ON i.invoice_id = il.invoice_id
WHERE il.track_id IN (
SELECT track_id FROM track$ t
JOIN genre$ g ON t.genre_id = g.genre_id
WHERE g.name LIKE 'Rock'
)
ORDER BY email
```

### 9. Which artists have the highest number of tracks sold?

```SQL
SELECT a.name, COUNT(c.track_id) AS track_count
FROM artist$ a
JOIN album$ b ON a.artist_id = b.artist_id
JOIN track$ c ON b.album_id = c.album_id
JOIN invoice_line$ d ON c.track_id = d.track_id
GROUP BY a.name
ORDER BY track_count DESC;
```
### 9. Which artists who have written the most rock music in our dataset. 
[Write a query that returns the Artist name and total track count of the top 10 rock bands. ]

```sql
SELECT c.artist_id, c.name, COUNT(*) AS number_of_songs
FROM track$ a
JOIN album$ b ON b.album_id = a.album_id
JOIN artist$ c ON c.artist_id = b.artist_id
JOIN genre$ d ON d.genre_id = a.genre_id
WHERE d.name LIKE 'Rock'
GROUP BY c.artist_id,c.name
ORDER BY number_of_songs DESC
```
