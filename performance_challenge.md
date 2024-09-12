# Performance Chllange

Goal: improve query performance

Steps:

1. Load the movr database

```
cockroach workload init movr --drop  \
    --num-histories 250000 --num-promo-codes 250000 --num-rides 125000  \
    --num-users 12500 --num-vehicles 3750  \
    "postgresql://craig:cockroach@<YOUR_CLUSTER_DNS>:26257"
```

Once the movr database is loaded, find a user that have more than 5 records in the `users` table.

```
SELECT name, COUNT(*) FROM users GROUP BY name HAVING COUNT(*) > 5;
```

Sample query result:  

         name         | count
----------------------+--------
  Michael Smith       |     9
  David Smith         |     7
  David Johnson       |     6
  Michael Davis       |     8
  Jennifer Williams   |     6
  Christopher Johnson |     7
  Joseph Johnson      |     6

Copy any `name` column value to be used in the following queryies.  

2. Optimize following workload.

```
SELECT * FROM users WHERE name = '<name_value_here>';  
```


SELECT name, credit_card FROM users WHERE name = 'Cheyenne Smith';

DROP INDEX users_name_idx;

CREATE INDEX ON users (name) STORING (credit_card);


Using EXPLAIN statement, find optimization opportunities to improve performance
Three workloads to improve:
Select * with a WHERE condition
Select two columns with a WHERE condition
Execute a JOIN statement of two tables
