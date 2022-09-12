### Notes from [SQL for Data Analysis](https://youtu.be/l8DCPaHc5TQ)

- In SQL, put the names containing empty spaces inside of back ticks 
  
```sql
USE `awesome chocolates data`;
```

- The `AS` keyword can be omitted. The following two queries are identical:
  
```sql
SELECT amount, boxes, amount / boxes AS 'amount per box' from sales;
```

```sql
SELECT amount, boxes, amount / boxes 'amount per box' from sales;
```

- https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html

- `IN` can replace `OR`:

```sql
SELECT * FROM people
WHERE team = 'delish' OR team = 'jucies';
```

```sql
SELECT * FROM people
WHERE team IN ('delish','jucies');
```

- `CASE` operator and branching logic:

```sql
SELECT SaleDate, Amount,
CASE 
WHEN amount < 1000 then 'Under 1k'
WHEN amount < 5000 then 'Under 5k'
WHEN amount < 10000 then 'Under 10k'
ELSE '10k or more'
END AS 'Amount category'
FROM sales;
```

- Adding conditions to `JOIN`s:

```sql
SELECT s.saleDate, s.amount, p.salesPerson, pr.product, p.team, g.geo
FROM sales s 
JOIN people p ON p.SPID = s.SPID
JOIN products pr ON pr.pid = s.pid 
JOIN geo g ON g.geoId = s.geoId
WHERE s.amount < 500
AND p.team = ''
AND g.geo IN ('New Zealand', 'India')
ORDER BY saleDate
```

- `GROUP BY` and creating reports with SQL:

```sql
SELECT geoId, sum(amount), avg(amount), sum(boxes)
FROM sales 
GROUP BY geoId;
```

```sql
SELECT pr.category, p.team, sum(boxes), sum(amount)
FROM sales s 
JOIN people p ON p.SPID = s.SPID
JOIN products pr ON pr.PID = s.PID 
WHERE p.team <> ''
GROUP BY pr.category, p.team
ORDER BY pr.category, p.team;
```
- Show top 10 products by amount:

```sql
SELECT pr.product, sum(s.amount) AS 'Total amount'
FROM sales s 
JOIN products pr ON pr.PID = s.PID 
GROUP BY pr.product 
ORDER BY 'Total amount' DESC
LIMIT 10;
```


