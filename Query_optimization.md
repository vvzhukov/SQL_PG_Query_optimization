# SQL_Query_optimization_basics
ANSI sql 

1. Avoid extra data retriving
```sql
-- wrong way
SELECT * FROM users WHERE age > 20;
-- better way
SELECT id, last_name, sex, age FROM users WHERE age > 20;
```
```sql
-- wrong way:
SELECT name, price FROM products;
-- better way:
SELECT name, price FROM products LIMIT 10;
```
2. Minimize functions on Left Hand-Side of the Operator
```sql
-- wrong way:
SELECT nickname FROM users WHERE DATEDIFF(MONTH, appointment_date, '2015-04-28') < 0;
-- better way:
SELECT nickname FROM users WHERE appointment_date > '2015-04-30';
```
3. Get rid of subqueries
```sql
-- wrong way:
SELECT user_id, last_name FROM users WHERE EXISTS (SELECT * FROM donationuser WHERE donationuser.user_id = users.user_id);
-- better* way:
SELECT DISTINCT users.user_id FROM users INNER JOIN donationuser ON users.user_id = donationuser.user_id;
-- * with an exception for empty data retieving Joe Celko explains it in one of his books that 
-- if you aren't returning data from the table, it is more efficient to use the IN predicate than to JOIN it
```
4. LIKE `%` is very expensive
```sql
-- wrong way:
SELECT * FROM users WHERE name LIKE '%bar%';
-- better way:
SELECT * FROM users WHERE name LIKE 'bar%';
```
5. Investigate slow querys
- Keep an eye on indexes.
- Avoid: non-indexed full table scans, non-indexed joins.
- Check and optimize queries.
- Caching could be really powerfull (especially for MySql).
- Sometimes it is better to merge data .
- Denormalize data by creating new tables. Sometimes it may significantly imrpove working speed (don't forget about triggers on parent tables, so that data consistency will be saved. Double check on using this one.
