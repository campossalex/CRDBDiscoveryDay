# Resilience Challange

Goal: run a SELECT query with cluster nodes down

Use the self-service disruption tool to take nodes down:  

http://3.133.120.37:5000/

You will need to get your cluster id to use the tool. In your cluster page, go to `Actions`, `Get Suppport` options and copy the `Cluster Support ID` value:  

<img width="551" alt="Screenshot 2024-09-20 at 13 13 46" src="https://github.com/user-attachments/assets/4a199719-e5ec-4e56-b3c5-422668b9c01c">

Once in the tool, use the `Disrupt` button on the Cluster Nodes table to take one node down at time. To restore all nodes, use the `Restore All Nodes` button located below the table.

<img width="1430" alt="Screenshot 2024-09-20 at 13 39 28" src="https://github.com/user-attachments/assets/4b1a2d42-6be9-4017-ba53-66e64ae1a910">

💡 Take any node down, run a simple SELECT query (SELECT * FROM movr.rides LIMIT 50;) and see if it returns records.   
💡 Use the DB Console -> Overview to see the alters listed when the node is down.  
