# Scalability Challange

Goal: run a workload while scaling up the cluster


## Run a workload  

CockroachDB binaries includes samples workloads to facilitates benchmarking and stress tests. To see how the databases behaviors during a scale up operation, run the `bank` workload. 
Copy the command and paste it in the `_Terminal` tab in Instruqt. Replace the <YOUR_CLUSTER_DNS> value:  

```
cockroach workload run bank --duration 15m --drop "postgresql://craig:cockroach@<YOUR_CLUSTER_DNS>:26257" --method simple_protocol --min-conns 500
```

After the inital table creation and data is loaded, you will see an output similar to the following one:  

```
_elapsed___errors__ops/sec(inst)___ops/sec(cum)__p50(ms)__p95(ms)__p99(ms)_pMax(ms)
    1.0s        0          112.1          141.0     39.8    906.0   1006.6   1006.6 transfer
    2.0s        0          482.0          311.5     46.1     62.9   1040.2   1140.9 transfer
    3.0s        0          464.8          362.6     46.1     60.8     75.5    167.8 transfer
    4.0s        0          446.1          383.5     48.2     65.0    113.2    243.3 transfer
    5.0s        0          397.7          386.3     50.3     83.9    125.8    285.2 transfer
    6.0s        0          334.3          377.6     54.5    159.4    184.5    251.7 transfer
    7.0s        0          473.9          391.4     46.1     65.0     96.5    134.2 transfer
    8.0s        0          482.9          402.8     44.0     60.8     75.5     79.7 transfer
```

## Scale up the Cluster

Your cluster is configured with one node. This is not a recommended configuration for production clusters, 
but for the propurse of this workshop, this setup is ok to demostrate how fast and easy a cluster can scale up.  

Go to the your cluster in the Cockroach Cloud console. Make sure you are in the `Overview` section. You should see a page like this:  

In the Overview page, click on the `pencil` icon you can see in the `Region` section. This will open a new page to edit the cluster configuration.

<img width="1073" alt="Screenshot 2024-10-22 at 04 27 33" src="https://github.com/user-attachments/assets/5dbdd715-1cd2-4118-a02a-0313bbf8f89e">

In the `Nodes` dropmenu option, select 3 value. This will add two more nodes to your cluster. 

<img width="791" alt="Screenshot 2024-10-22 at 04 27 55" src="https://github.com/user-attachments/assets/a73e8b3b-7a86-405b-918c-ac0babf7ddcc">

⚠️ Do not add a new Region. Just change from 1 to 3 the Nodes value.

On the right-hand side, click on `Next: Capacity` button and move to the Capacity section.

Do not make any changes on the Capacity section, click on `Update Cluster` to finsh the scale up configuration. So easy, right?

Your cluster will be in `Maintenance` mode to process the scale up and add the two additional nodes. 

<img width="539" alt="Screenshot 2024-10-22 at 04 32 42" src="https://github.com/user-attachments/assets/e538465f-70a5-4c13-8210-4bb8e1c6f578">

⚠️ The scale up process will take from 4 to 6 minutes to finish.  

While the the cluster is scaling up, check the following:  

💡 Use the DB Console to monitor the scale up process.  
💡 Check the workload you are running in `_Terminal` and observe if the workload was stopped while scaling up the cluster.  

When the scale up process is finished, you can see the two added nodes, indicating 3/3 live nodes.

<img width="537" alt="Screenshot 2024-10-22 at 04 37 04" src="https://github.com/user-attachments/assets/09d43667-90d0-4f85-99fe-d5b1430dcc64">
