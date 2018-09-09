#Execution Plan for PG SQL
Retriving the Execution Plan:
```sql
EXPLAIN SELECT * FROM user;

QUERY PLAN
----------------------------------------------------------
 Seq Scan on users  (cost=0.00..5.24 rows=234 width=41)
```
Statement is not executed and we only get a prediction of what is likely to happen.
We can use `ANALYZE` keyword which does actually run the query and which prints more detailed information to the output:
```sql
EXPLAIN ANALYZE SELECT * FROM users;
 
QUERY PLAN
-----------------------------------------------------------
Seq Scan on users (cost=0.00..5.21 rows=173 width=118)
         (actual time=0.018..0.018 rows=0 loops=1)
 Total runtime: 0.020 ms
```
You can also run `ANALYZE` on other DML operators. Keep in mind that the statement will be executed.
We can avoid that by wrapping statement in transaction:
```sql
BEGIN;
EXPLAIN ANALYZE ...;
ROLLBACK;
```
