# HIGHEST SALES REVENUE -

### GENRE-
```sql

SELECT 
G.name AS Genre_name, 
SUM(IL.unit_price * IL.quantity) AS Revenue
FROM genre$ G
JOIN track$ T 
    ON G.genre_id = T.genre_id
JOIN invoice_line$ IL 
    ON T.track_id = IL.track_id
GROUP BY G.name
ORDER BY Revenue DESC
```

### MEDIA_TYPE -
```SQL
SELECT 
M.name AS MEDIA_name, 
SUM(IL.unit_price * IL.quantity) AS Revenue
FROM media_type$ M
JOIN track$ T 
   ON M.media_type_id = T.media_type_id
JOIN invoice_line$ IL
   ON T.track_id = IL.track_id
GROUP BY M.name
ORDER BY Revenue DESC
```

### ALBUM -
```SQL
SELECT 
AL.title,
SUM(IL.unit_price * IL.quantity) AS total_revenue
FROM album$ AS AL 
JOIN track$ AS T 
    ON AL.album_id = T.album_id
JOIN invoice_line$ AS IL 
   ON T.track_id = IL.track_id
GROUP BY AL.title
ORDER BY total_revenue DESC;
```

### ARTIST -
```SQL
SELECT 
AR.artist_id, 
AR.name, 
SUM(IL.unit_price * IL.quantity) AS total_revenue
FROM artist$ AR
JOIN album$ AL 
   ON AR.artist_id = AL.artist_id
JOIN track$ T 
   ON AL.album_id = T.album_id
JOIN invoice_line$ IL ON T.track_id = IL.track_id
GROUP BY AR.artist_id, AR.name
ORDER BY total_revenue DESC;
```
### PLAYLIST -
```SQL
SELECT 
P.name,
SUM(il.unit_price * il.quantity) AS total_revenue
FROM playlist$ P
JOIN playlist_track$ PT 
  ON PT.playlist_id = P.playlist_id
JOIN track$ AS T 
  ON PT.track_id = T.track_id
JOIN invoice_line$ AS il
  ON t.track_id = il.track_id
GROUP BY P.name
ORDER BY total_revenue DESC;
```
### TRACKS -
```SQL
SELECT 
T.name ,
SUM(il.unit_price * il.quantity) AS total_revenue
FROM track$ AS T
JOIN invoice_line$ AS il
  ON t.track_id = il.track_id
GROUP BY T.name
ORDER BY total_revenue DESC;
```


# TOTAL SALES - [ What are the top 5 best-selling albums of all time]


### GENRE-
```SQL
SELECT G.name, SUM(il.quantity) AS total_sales
FROM genre$ AS G
JOIN track$ AS t ON G.genre_id= t.genre_id
JOIN invoice_line$ AS il ON t.track_id = il.track_id
GROUP BY G.name
ORDER BY total_sales DESC
```

### MEDIA_TYPE -
```SQL
SELECT M.name, SUM(il.quantity) AS total_sales
FROM media_type$ AS M
JOIN track$ AS t ON M.media_type_id= t.media_type_id
JOIN invoice_line$ AS il ON t.track_id = il.track_id
GROUP BY M.name
ORDER BY total_sales DESC
```
### ALBUMS -
```SQL
SELECT 
AL.title,
SUM(il.quantity) AS total_sales
FROM album$ AS AL 
JOIN track$ AS T 
    ON AL.album_id = T.album_id
JOIN invoice_line$ AS IL 
   ON T.track_id = IL.track_id
GROUP BY AL.title
ORDER BY total_sales DESC;
```

### ARTIST -
```SQL
SELECT 
AR.artist_id, 
AR.name, 
SUM(il.quantity) AS total_sales
FROM artist$ AR
JOIN album$ AL 
   ON AR.artist_id = AL.artist_id
JOIN track$ T 
   ON AL.album_id = T.album_id
JOIN invoice_line$ IL ON T.track_id = IL.track_id
GROUP BY AR.artist_id, AR.name
ORDER BY total_sales DESC;
```

### PLAYLIST -
```SQL
SELECT 
P.name,
SUM(il.quantity) AS total_sales
FROM playlist$ P
JOIN playlist_track$ PT 
  ON PT.playlist_id = P.playlist_id
JOIN track$ AS T 
  ON PT.track_id = T.track_id
JOIN invoice_line$ AS il
  ON t.track_id = il.track_id
GROUP BY P.name
ORDER BY total_sales DESC;
```
### TRACKS -
```SQL
SELECT 
T.name ,
SUM(il.quantity) AS total_sales
FROM track$ AS T
JOIN invoice_line$ AS il
  ON t.track_id = il.track_id
GROUP BY T.name
ORDER BY total_sales DESC;
```

# POPULARITY AMONG CUSTOMERS -

### GENRE-
```SQL
SELECT COUNT(C.customer_id) AS NO_OF_CUSTOMERS ,G.name 
FROM customer$ C
JOIN invoice$ i ON c.customer_id = i.customer_id
JOIN invoice_line$ il ON i.invoice_id = il.invoice_id
JOIN track$ AS T ON IL.track_id = T.track_id
JOIN genre$ AS G 
    ON G.genre_id = T.genre_id
	GROUP BY G.name 
ORDER BY NO_OF_CUSTOMERS DESC
```

### MEDIA_TYPE -
```SQL
SELECT COUNT(C.customer_id) AS NO_OF_CUSTOMERS ,M.name 
FROM customer$ C
JOIN invoice$ i ON c.customer_id = i.customer_id
JOIN invoice_line$ il ON i.invoice_id = il.invoice_id
JOIN track$ AS T ON IL.track_id = T.track_id
JOIN media_type$ AS M 
    ON M.media_type_id = T.media_type_id
	GROUP BY M.name  
ORDER BY NO_OF_CUSTOMERS DESC
```
### ALBUMS -
```SQL
SELECT COUNT(C.customer_id) AS NO_OF_CUSTOMERS ,AL.name 
FROM customer$ C
JOIN invoice$ i ON c.customer_id = i.customer_id
JOIN invoice_line$ il ON i.invoice_id = il.invoice_id
JOIN track$ AS T ON IL.track_id = T.track_id
JOIN ALBUM$ AS AL 
    ON AL.ALBUM_ID = T.ALBUM_ID
	GROUP BY AL.name   
ORDER BY NO_OF_CUSTOMERS DESC
```

### ARTIST -
```SQL

SELECT COUNT(C.customer_id) AS NO_OF_CUSTOMERS ,AR.name 
FROM customer$ C
JOIN invoice$ i ON c.customer_id = i.customer_id
JOIN invoice_line$ il ON i.invoice_id = il.invoice_id
JOIN track$ AS T ON IL.track_id = T.track_id
JOIN ALBUM$ AS AL ON AL.ALBUM_ID = T.ALBUM_ID
JOIN artist$ AR ON AR.artist_id = AL.artist_id
	GROUP BY AR.name   
ORDER BY NO_OF_CUSTOMERS DESC
```

### PLAYLIST -
```SQL

SELECT COUNT(C.customer_id) AS NO_OF_CUSTOMERS ,P.name
FROM customer$ C
JOIN invoice$ i ON c.customer_id = i.customer_id
JOIN invoice_line$ il ON i.invoice_id = il.invoice_id
JOIN track$ AS T ON IL.track_id = T.track_id
JOIN playlist_track$ PT ON PT.track_id = T.track_id
JOIN playlist$ P ON P.playlist_id = PT.playlist_id
	GROUP BY P.name   
ORDER BY NO_OF_CUSTOMERS DESC
```
### TRACKS -
```SQL
SELECT COUNT(C.customer_id) AS NO_OF_CUSTOMERS ,T.name
FROM customer$ C
JOIN invoice$ i ON c.customer_id = i.customer_id
JOIN invoice_line$ il ON i.invoice_id = il.invoice_id
JOIN track$ AS T ON IL.track_id = T.track_id
GROUP BY T.name   
ORDER BY NO_OF_CUSTOMERS DESC
```




# POPULARITY IN COUNTRIES -

### GENRE-
```SQL
SELECT
  g.name AS genre_name,
  i.billing_country,
  COUNT(t.track_id) AS track_count
FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS t ON t.track_id = il.track_id
JOIN genre$ g ON g.genre_id = t.genre_id
GROUP BY g.name, i.billing_country
HAVING COUNT(t.track_id) =
(SELECT MAX(track_count) FROM
      (
        SELECT
          g.name AS genre_name,
          i.billing_country,
          COUNT(t.track_id) AS track_count
        FROM  invoice$ AS i
  join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS t ON t.track_id = il.track_id
JOIN  genre$ g ON g.genre_id = t.genre_id
GROUP BY g.name, i.billing_country) AS subquery
    WHERE subquery.billing_country = i.billing_country )
ORDER BY track_count desc,
  i.billing_country;
```
----------------------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------------------

```SQL
 WITH popular_genres AS (
  SELECT
    g.name AS genre_name,
    i.billing_country,
    COUNT(t.track_id) AS track_count,
    ROW_NUMBER() OVER (PARTITION BY i.billing_country ORDER BY COUNT(t.track_id) DESC) AS rank
  FROM
    invoice$ AS i
    JOIN invoice_line$ il ON il.invoice_id = i.invoice_id
    JOIN track$ AS t ON t.track_id = il.track_id
    JOIN genre$ g ON g.genre_id = t.genre_id
  GROUP BY
    g.name, i.billing_country
)
SELECT
  genre_name,
  billing_country,
  track_count
FROM
  popular_genres
WHERE
  rank = 1
ORDER BY
  track_count DESC,
  billing_country;
  ```

### MEDIA_TYPE -
```SQL
SELECT M.name,  i.billing_country,COUNT(t.track_id) AS track_count 
 FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
join media_type$ M  on M.media_type_id = T.media_type_id
GROUP BY  M.name,  i.billing_country
HAVING COUNT(t.track_id) = (SELECT MAX(track_count) FROM 
                                                       ( SELECT M.name,  i.billing_country,COUNT(t.track_id) AS track_count 
                                                         FROM invoice$ AS i
                                                         join invoice_line$ il on il.invoice_id = i.invoice_id
                                                         JOIN track$ AS T ON T.track_id = il.track_id
                                                         join media_type$ M  on M.media_type_id = T.media_type_id
                                                         GROUP BY  M.name,  i.billing_country)
                                                                                                AS SUB
                              WHERE SUB.billing_country = I.billing_country)
ORDER BY track_count desc,
  i.billing_country;
```
----------------------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------------------

```SQL
  WITH popular_genres AS (
  SELECT
    M.name AS MEDIA_TYEPE_NAME,
    i.billing_country,
    COUNT(t.track_id) AS track_count,
    ROW_NUMBER() OVER (PARTITION BY i.billing_country ORDER BY COUNT(t.track_id) DESC) AS rank
  
   FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
join media_type$ M  on M.media_type_id = T.media_type_id
  GROUP BY
    M.name, i.billing_country
)
SELECT
  MEDIA_TYEPE_NAME,
  billing_country,
  track_count
FROM
  popular_genres
WHERE
  rank = 1
ORDER BY
  track_count DESC,
  billing_country;

```
### ALBUMS -
```SQL

  SELECT AL.title,  i.billing_country,COUNT(t.track_id) AS track_count 
 FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
join album$ AL  on AL.album_id = T.album_id
GROUP BY   AL.title,  i.billing_country
HAVING COUNT(t.track_id) = (SELECT MAX(track_count) FROM 
   (SELECT AL.title,  i.billing_country,COUNT(t.track_id) AS track_count 
 FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
join album$ AL  on AL.album_id = T.album_id
GROUP BY   AL.title,  i.billing_country)
AS SUB
 WHERE SUB.billing_country = I.billing_country)
ORDER BY track_count desc,
  i.billing_country;
```
----------------------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------------------------------------------------

```sql
WITH popular_genres AS (
  SELECT
    AL.title AS SDS_TYEPE_NAME,
    i.billing_country,
    COUNT(t.track_id) AS track_count,
    DENSE_RANK() OVER (PARTITION BY i.billing_country ORDER BY COUNT(t.track_id) DESC) AS rank -- Use DENSE_RANK to handle ties
  --If we use Row_number() it would assign a rank for every country even if they have same trackcount but we want all trackcounts by city
  FROM invoice$ AS i
  JOIN invoice_line$ il ON il.invoice_id = i.invoice_id
  JOIN track$ AS T ON T.track_id = il.track_id
  JOIN album$ AL ON AL.album_id = T.album_id
  GROUP BY
    AL.title, i.billing_country
)
SELECT
  SDS_TYEPE_NAME,
  billing_country,
  track_count
FROM
  popular_genres
WHERE
  rank = 1
ORDER BY
  track_count DESC,
  billing_country;
  ```

### ARTIST -
```SQL

SELECT  ar.name ,  i.billing_country,COUNT(t.track_id) AS track_count 
 FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
join album$ AL  on AL.album_id = T.album_id
join artist$ ar  on ar.artist_id = al.artist_id
GROUP BY  ar.name ,  i.billing_country
HAVING COUNT(t.track_id) = (SELECT MAX(track_count) FROM 
   ( SELECT  ar.name ,  i.billing_country,COUNT(t.track_id) AS track_count 
 FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
join album$ AL  on AL.album_id = T.album_id
join artist$ ar  on ar.artist_id = al.artist_id
GROUP BY   ar.name ,  i.billing_country)
    AS SUB
 WHERE SUB.billing_country = I.billing_country)
ORDER BY track_count desc,
  i.billing_country;
```
-------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------------------

```sql
  WITH popular_genres AS (
  SELECT
   ar.name AS ALBUM_NAME,
    i.billing_country,
    COUNT(t.track_id) AS track_count,
    dense_rank() OVER (PARTITION BY i.billing_country ORDER BY COUNT(t.track_id) DESC) AS rank
 FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
join album$ AL  on AL.album_id = T.album_id
join artist$ ar  on ar.artist_id = al.artist_id
GROUP BY  ar.name,  i.billing_country
)
SELECT
  ALBUM_NAME,
  billing_country,
  track_count
FROM
  popular_genres
WHERE
  rank = 1
ORDER BY
  track_count DESC,
  billing_country;
```

### PLAYLIST -
```SQL


SELECT  p.name ,  i.billing_country,COUNT(t.track_id) AS track_count 
 FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
JOIN playlist_track$ PT ON PT.track_id = T.track_id
JOIN playlist$ P ON P.playlist_id = PT.playlist_id
GROUP BY  p.name ,  i.billing_country
HAVING COUNT(t.track_id) = (SELECT MAX(track_count) FROM 
       ( SELECT  p.name ,  i.billing_country,COUNT(t.track_id) AS track_count 
 FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
JOIN playlist_track$ PT ON PT.track_id = T.track_id
JOIN playlist$ P ON P.playlist_id = PT.playlist_id
GROUP BY  p.name ,  i.billing_country
) AS SUB
WHERE SUB.billing_country = I.billing_country)
ORDER BY track_count desc,
  i.billing_country;
```
-------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------------------
```sql
  WITH popular_genres AS (
  SELECT
   p.name AS ALBUM_NAME,
    i.billing_country,
    COUNT(t.track_id) AS track_count,
    dense_rank() OVER (PARTITION BY i.billing_country ORDER BY COUNT(t.track_id) DESC) AS rank
 FROM invoice$ AS i
join invoice_line$ il on il.invoice_id = i.invoice_id
JOIN track$ AS T ON T.track_id = il.track_id
JOIN playlist_track$ PT ON PT.track_id = T.track_id
JOIN playlist$ P ON P.playlist_id = PT.playlist_id
GROUP BY  p.name ,  i.billing_country
)
SELECT
  ALBUM_NAME,
  billing_country,
  track_count
FROM
  popular_genres
WHERE
  rank = 1
ORDER BY
  track_count DESC,
  billing_country
```
### TRACKS -
```SQL
SELECT COUNT(C.customer_id) AS NO_OF_CUSTOMERS ,T.name
FROM customer$ C
JOIN invoice$ i ON c.customer_id = i.customer_id
JOIN invoice_line$ il ON i.invoice_id = il.invoice_id
JOIN track$ AS T ON IL.track_id = T.track_id
GROUP BY T.name   
ORDER BY NO_OF_CUSTOMERS DESC
```
















# EMPLOYEE_ANALYSIS : -

### 1. Who is the senior most employee based on job title -
```sql
SELECT  Top 1 * FROM employee$ 
ORDER BY hire_date ASC
```
### 2 .Which employees have the highest sales volume?

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

# CUSTOMER_ANALYSIS : -

### 1. Who are the top 10 highest-spending customers-
```SQL

SELECT 
c.customer_id, 
c.first_name + ' ' + c.last_name as Customer_name, 
SUM(i.total) AS total_spending
FROM customer$ AS c
JOIN invoice$ AS i
  ON c.customer_id = i.customer_id
GROUP BY c.customer_id, c.first_name, c.last_name
ORDER BY total_spending DESC
```
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
### 3. What is the average number of purchases per customer -

```SQL
SELECT AVG(purchase_count) AS average_purchases_per_customer
FROM (
    SELECT customer_id, COUNT(DISTINCT invoice_id) AS purchase_count
    FROM invoice$
    GROUP BY customer_id
) AS customer_purchases;
```
### 4. Which countries have the highest number of customers -
```SQL
SELECT country, COUNT(*) AS customer_count
FROM customer$
GROUP BY country
ORDER BY customer_count DESC
```
### 5. What is the distribution of customers by geographic location?

```sql
select country , state,city,count(*) from customer$
group by country , state,city
```

### 6. Who is the best customer - 
[ The customer who has spent the most money will be declared the best customer]
```sql
SELECT customer_id,SUM(total) as SPEND
FROM invoice$
GROUP BY customer_id
order by SPEND desc
```

### 7. Write query to return the email, first name, last name, & Genre of all Rock Music listeners -

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
