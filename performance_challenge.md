# Performance Chllange

Goal: improve query performance

## Load sample data  

Before running the workloads, load the movr sample database following these steps:  

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

```
         name         | count
----------------------+--------
  Michael Smith       |     9
  David Smith         |     7
  David Johnson       |     6
  Michael Davis       |     8
  Jennifer Williams   |     6
  Christopher Johnson |     7
  Joseph Johnson      |     6
```

Copy any `name` column value, that be used in the following queries.  Suggestion: pick the user with the highest cardinality.   
Now it is time to run and optimize some workloads.   

## Workload A

```
SELECT * FROM users WHERE name = '<name_value_here>';  
```
The time of the first execution spans from 4 to 9 ms. Reduce that execution time.   

💡 Use the EXPLAIN statement to understand the query plan and spot optimization opportunties.  

## Workload B

```
SELECT name, credit_card FROM users WHERE name = '<name_value_here>'; 
```
The time of the first execution spans from 4 to 9 ms. Reduce that execution time.   

💡 Use the EXPLAIN statement to understand the query plan and spot optimization opportunties.  
💡 Use DROP INDEX <index_name> if you need to recreate and index.   


## Workload C

```
EXPLAIN SELECT  \  
    name, count(rides.id) AS sum  \  
FROM  \  
    users JOIN rides ON users.id = rides.rider_id  \  
WHERE  \  
    rides.start_time BETWEEN '2018-12-31 00:00:00' AND '2020-01-01 00:00:00'  \  
GROUP BY  \  
    name  \  
ORDER BY  \  
    sum DESC  \  
LIMIT  \  
    10;  \  
```
