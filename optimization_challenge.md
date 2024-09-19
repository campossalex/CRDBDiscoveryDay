# Optimization Chllange

Goal: distribute table ranges to avoid hot spots

## The "hot spot" issue

Follow these steps to 

1. Create the table with sequential primary key  
    
```
CREATE TABLE purchase_serial (
    id SERIAL PRIMARY KEY,
    amount DECIMAL NOT NULL
);
```

2. Change the range max size to 67 MiB or lower, so the table will split the data in more ranges faster.  
    
```
ALTER TABLE purchase_serial CONFIGURE ZONE USING 
    range_min_bytes = 0,
    range_max_bytes = 67108864;
```

3. Insert 2 million records. It can take 15 to 20 seconds to finish this operation.  

```
INSERT INTO purchase_serial (amount) 
SELECT round (random() * 100, 2) 
FROM generate_series (1, 2000000);
```

4. Now check how the table's data is distributed in ranges. Use the following statement to list the table's range with relevant information to analyse.  

```
SELECT range_id, range_size_mb, start_key, end_key, lease_holder, replicas FROM
[SHOW RANGES FROM TABLE purchase_serial WITH DETAILS]; 
```


5. Insert 2 million new records (step 3) and then list the table's ranges (step 4). Observe the following:  

   Size of the ranges?  
   Range's leaseholder node? Are they varying or most of the ranges are hosted in one same node?
   What problem are you able to detect with this workload?

5. Once again, insert 2 million new records (step 3) and then list the table's ranges (step 4).  

   💡 Use the Monitoring tools CockroachDB provides. While inserting the records, review the `Dashboard: Replication` page in Metrics.
   Look for the `Leaseholders per Node`chart on that page and observe how the chart line will change with each bulk insertion.

   What problem are you able to detect with this workload?

## Fix the "hot spot" issue  

```
SELECT * FROM users WHERE name = '<name_value_here>';  
```
The time of the first execution spans from 4 to 9 ms. Reduce that execution time.   

💡 Use the `EXPLAIN` statement to understand the query plan and find out optimization opportunities.  

## Workload B

```
SELECT name, credit_card FROM users WHERE name = '<name_value_here>'; 
```
The time of the first execution spans from 4 to 9 ms. Reduce that execution time.   

💡 Use the `EXPLAIN` statement to understand the query plan and find out optimization opportunities.  
💡 Use `DROP INDEX <index_name>` if you need to recreate and index.   


## Workload C

```
SELECT name, count(rides.id) AS sum  
FROM users JOIN rides ON users.id = rides.rider_id  
WHERE rides.start_time BETWEEN '2018-12-31 00:00:00' AND '2020-01-01 00:00:00'  
GROUP BY name  
ORDER BY sum DESC  
LIMIT 10; 
```
The time of the first execution spans from 40 to 100 ms. Reduce that execution time.   

💡 Use the `EXPLAIN` statement to understand the query plan and find out optimization opportunities.  
