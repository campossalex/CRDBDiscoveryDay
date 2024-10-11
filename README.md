# Welcome to CockroachDB Discovery Gay

## Networking setup

Before you start with the challenges, make sure you have access to DB Console and sql endpoint.

1. Navigate to your cluster's Networking > IP Allowlist tab.

   The IP Allowlist tab displays a list of authorized networks (i.e., an IP network allowlist) that can access the cluster.

2. Click the Add Network button.

   The Add Network dialog displays.

3. From the Network dropdown, select **Current Network** to auto-populate your local machine's IP address:

   If you are using an Instruqt machine to connect to your cluster, please run the following command in the CLI to get the machine Public IP address:

   ```
   curl -s checkip.dyndns.org | sed -e 's/.*Current IP Address: //' -e 's/<.*$//'
   ```

   <img width="557" alt="Screenshot 2024-10-02 at 06 38 53" src="https://github.com/user-attachments/assets/328646cd-f7db-4b57-9f8e-d624587a2de5">

   Make sure to mark both cluster's **DB Console to monitor the cluster** and **CockroachDB Client to access databases** options.

5. Add one more IP address, This time will be the network you are connected from your computer. Click the Add Network button.

6. From the Network dropdown, select Current Network to auto-populate your local machine's IP address:

   <img width="558" alt="Screenshot 2024-10-07 at 16 05 05" src="https://github.com/user-attachments/assets/9ca83ef0-24a6-4d1f-ab4b-b0a1680629e8">

   Make sure to mark the cluster's *DB Console to monitor the cluster* option.

5. Click Apply.

6. Just to make sure you are all set in the networking setup, you should be able to see two network IPs in the **IP Allowlist** tab.

   <img width="895" alt="Screenshot 2024-10-07 at 16 08 51" src="https://github.com/user-attachments/assets/ce3f7df9-d929-436c-8bfc-b57c63a98db0">


## SQL Client

You can use any SQL client of your choice, like Datagrip or DBeaver. The only requirements is to use Postres jdbc/odbc to connect to CRDB cluster.  
CockroackDB provides a shell client binary that you can install in Mac, Linux or Windows. Refer to the following [documentation](https://www.cockroachlabs.com/docs/stable/cockroach-sql-binary) to install CRDB sql client.  

On Cockroach Cloud, you can follow the instructions to connect using the IP Allowlist you just configured. Go to top-right corner, button Connect to open the instructions dialog.  

## Challenges

* [Performance Challenge](https://github.com/campossalex/CRDBGameGay/blob/main/performance_challenge.md)
* [Integration Challenge](https://github.com/campossalex/CRDBGameGay/blob/main/integration_challenge.md)
* [Resilience Challenge](https://github.com/campossalex/CRDBGameGay/blob/main/resilience_challenge.md)
* [Optimization Challenge](https://github.com/campossalex/CRDBGameGay/blob/main/optimization_challenge.md)
