````md
# Sales Insights Data Analysis Project

## Data Analysis Using SQL

### Show all customer records
```sql
SELECT * FROM customers;
````

### Show total number of customers

```sql
SELECT COUNT(*) FROM customers;
```

### Show transactions for Chennai market (market code for Chennai is Mark001)

```sql
SELECT * 
FROM transactions 
WHERE market_code = 'Mark001';
```

### Show distinct product codes that were sold in Chennai

```sql
SELECT DISTINCT product_code 
FROM transactions 
WHERE market_code = 'Mark001';
```

### Show transactions where currency is US Dollars

```sql
SELECT * 
FROM transactions 
WHERE currency = 'USD';
```

### Show transactions in 2020 (joined with date table)

```sql
SELECT t.*, d.*
FROM transactions t
INNER JOIN date d 
    ON t.order_date = d.date
WHERE d.year = 2020;
```

### Show total revenue in year 2020 (INR + USD)

```sql
SELECT SUM(t.sales_amount)
FROM transactions t
INNER JOIN date d 
    ON t.order_date = d.date
WHERE d.year = 2020
  AND (t.currency = 'INR' OR t.currency = 'USD');
```

### Show total revenue in January 2020

```sql
SELECT SUM(t.sales_amount)
FROM transactions t
INNER JOIN date d 
    ON t.order_date = d.date
WHERE d.year = 2020
  AND d.month_name = 'January'
  AND (t.currency = 'INR' OR t.currency = 'USD');
```

### Show total revenue in year 2020 in Chennai

```sql
SELECT SUM(t.sales_amount)
FROM transactions t
INNER JOIN date d 
    ON t.order_date = d.date
WHERE d.year = 2020
  AND t.market_code = 'Mark001';
```

---

## Data Analysis Using Power BI

### Formula to create norm_amount column

```m
= Table.AddColumn(
    #"Filtered Rows",
    "norm_amount",
    each if [currency] = "USD" or [currency] = "USD#(cr)" 
         then [sales_amount] * 75 
         else [sales_amount],
    type any
)
```

```


