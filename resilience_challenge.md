# Resilience Challange

Goal: run a workload while disrupting cluster nodes

## Get your cluster ID:

You will need to get your cluster id to use the tool. In your cluster page, go to `Actions`, `Get Suppport` options and copy the `Cluster Support ID` value:  

<img width="551" alt="Screenshot 2024-09-20 at 13 13 46" src="https://github.com/user-attachments/assets/4a199719-e5ec-4e56-b3c5-422668b9c01c">

## Cluster disruption tool

Use the self-service disruption tool to take nodes down (open is a new tab):  

[Open cluster disruption tool](http://18.119.119.45:5000/)

Once in the tool, paste the cluster ID you copied before and click `Submit`: 

<img width="843" alt="Screenshot 2024-10-21 at 21 02 16" src="https://github.com/user-attachments/assets/983762d3-e548-4645-b1a5-305613da8a9e">

Once in the tool, this is how it works:  
- `Disrupt` button on the Cluster Nodes table to take one node down at time.
- `Restore All Nodes` button to restore all nodes.

<img width="1430" alt="Screenshot 2024-09-20 at 13 39 28" src="https://github.com/user-attachments/assets/4b1a2d42-6be9-4017-ba53-66e64ae1a910">

## Run the Go Application

There is a Go Application already loaded in Instuqt. This applicaiton manages Transactions, so when a nodes is down, the application skips the failed operation, avoiding the whole application to fail.  

In Instruqt, go the the `Application` tab, and on the left-hand side, click on the file `main.go`. The code will open on the center panel editor.  You don't need to make changes, this is just for your reference.  

To execute the application, go back to the `_Terminal` tab in Instruqt and run the following commands:  

Change to the directory where the actually application is loaded:  
```
cd go_application
```

Run the Go application. Change <YOUR_CLUSTER_DNS> value for your actual cluster DNS:  
```
go run main.go -url "postgresql://craig:cockroach@<YOUR_CLUSTER_DNS>:26257/defaultdb"
```

You will start to see something like this:  

```
7557d3d6 -> 6a59f6b9 took 440ms
c4a15fab -> 66175acf took 191ms
71cf7285 -> e087576b took 188ms
b681fb41 -> fe2259dd took 200ms
847b3986 -> 0fd897c8 took 198ms
```

The Go application will create a table called `account` in `defaultdb` database with some initial recods, and randomly will transfer money from one account to other.  

Now it is time to see and play with Resilience.  

💡 Take any node down while running the Go application.   
💡 If the node down, run a simple SELECT query (SELECT * FROM default.account LIMIT 50;) and see if it returns records.   
💡 Use the DB Console -> Overview to see the alters listed when the node is down.  
