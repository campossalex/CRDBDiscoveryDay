# Resilience Challange

Goal: run a workload while disrupting cluster nodes

1. Get your cluster ID:

Use the self-service disruption tool to take nodes down:  

http://3.133.120.37:5000/

You will need to get your cluster id to use the tool. In your cluster page, go to `Actions`, `Get Suppport` options and copy the `Cluster Support ID` value:  

<img width="551" alt="Screenshot 2024-09-20 at 13 13 46" src="https://github.com/user-attachments/assets/4a199719-e5ec-4e56-b3c5-422668b9c01c">

2. Cluster disruption tool

<img width="843" alt="Screenshot 2024-10-21 at 21 02 16" src="https://github.com/user-attachments/assets/983762d3-e548-4645-b1a5-305613da8a9e">


Once in the tool, this is how it works:  
- `Disrupt` button on the Cluster Nodes table to take one node down at time.
- `Restore All Nodes` button to restore all nodes.

<img width="1430" alt="Screenshot 2024-09-20 at 13 39 28" src="https://github.com/user-attachments/assets/4b1a2d42-6be9-4017-ba53-66e64ae1a910">




💡 Take any node down, run a simple SELECT query (SELECT * FROM movr.rides LIMIT 50;) and see if it returns records.   
💡 Use the DB Console -> Overview to see the alters listed when the node is down.  
