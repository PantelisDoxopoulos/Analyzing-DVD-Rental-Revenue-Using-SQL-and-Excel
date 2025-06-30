# 🎬 Sakila Revenue Dashboard (Beginner SQL & Excel Project)

## 📌 Project Overview

This is a beginner-level data analysis project using the **Sakila DVD Rental database**, where I queried the data using **SQL** and visualized the results using **Microsoft Excel**. The goal of the project was to explore **revenue patterns**, identify **top customers**, and gain business insights from rental data.

> ✅ This project was completed in **one day** as a personal learning exercise.  
> 💡 It was designed to strengthen my skills in SQL querying, data cleaning, and Excel dashboard creation.

---

## 🛠️ Tools Used
- **PostgreSQL** for SQL queries  
- **Excel** for data visualization and dashboard creation  
- No Power Pivot was used — all visualizations are based on **static data exports**

---

## 📊 Key Visualizations & Queries

###  1. Total Revenue and Number of Payments
- Displays total revenue and total number of purchases.
```sql
SELECT SUM(amount) AS total_revenue
FROM payment;
```

### 2. **Revenue per Month**
- Shows revenue for each month in 2007.
```sql
SELECT TO_CHAR(payment_date,'MONTH') as Month,
       SUM(amount) AS monthly_revenue
FROM payment
GROUP BY month
ORDER BY MIN(EXTRACT(MONTH FROM payment_date));
```

### 3. **Top 10 customers**
- Identifies the most valuable customers based on total amount paid.
```sql
SELECT first_name, last_name,
       COUNT(amount) AS number_of_payments,
       SUM(amount) AS total_paid
FROM customer
INNER JOIN payment ON customer.customer_id = payment.customer_id
GROUP BY first_name, last_name
ORDER BY SUM(amount) DESC
LIMIT 10;
```

### 4. **Top 5 movies**
```sql
SELECT title AS movie_title, name AS category_name, SUM(amount) AS total_revenue
FROM film
INNER JOIN film_category ON film.film_id = film_category.film_id
INNER JOIN category ON category.category_id = film_category.category_id
INNER JOIN inventory ON inventory.film_id = film.film_id
INNER JOIN rental ON rental.inventory_id = inventory.inventory_id
INNER JOIN payment ON payment.rental_id = rental.rental_id
GROUP BY title, name
ORDER BY SUM(amount) DESC
LIMIT 5;
```

### 5. **Top 5 cities by revenue**
```sql
SELECT city, SUM(amount) AS total_revenue
FROM payment
INNER JOIN customer ON payment.customer_id = customer.customer_id
INNER JOIN address ON address.address_id = customer.address_id
INNER JOIN city ON city.city_id = address.city_id
GROUP BY city
ORDER BY SUM(amount) DESC
LIMIT 5;
```

### 5. **Top 5 countries by revenue**
```sql
SELECT country, SUM(amount) AS total_revenue
FROM payment


INNER JOIN customer ON payment.customer_id = customer.customer_id
INNER JOIN address ON address.address_id = customer.address_id
INNER JOIN city ON city.city_id = address.city_id
INNER JOIN country ON country.country_id = city.country_id
GROUP BY country
ORDER BY SUM(amount) DESC
LIMIT 5;
```


## 📁 What's Included
- ✅ Excel file with all charts and dashboard visuals
- ✅ Screenshot of the final dashboard
- ✅ This `README.md` with all queries and explanations

---

## 🧠 Reflections
- I completed this project to improve my SQL and Excel skills.
- No relationships were built across tables for slicers, since most tables did not have shared keys.
- In the future, I’d like to explore Power BI or Power Pivot for more interactive dashboards.
