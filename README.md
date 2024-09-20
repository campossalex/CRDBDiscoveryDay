# Welcome to CockroachDB Game Gay

## Networking setup

Before you start with the challenges, make sure you have access to DB Console and sql endpoint.

1. Navigate to your cluster's Networking > IP Allowlist tab.

   The IP Allowlist tab displays a list of authorized networks (i.e., an IP network allowlist) that can access the cluster.

2. Click the Add Network button.

   The Add Network dialog displays.

3. From the Network dropdown, select **Current Network** to auto-populate your local machine's IP address:

   <img width="539" alt="Screenshot 2024-09-13 at 11 05 17" src="https://github.com/user-attachments/assets/f4972220-a32d-4504-9f51-9fd28305cb55">

   Make sure to mark both cluster's **DB Console to monitor the cluster** and **CockroachDB Client to access databases** options.

4. Click Apply.

## SQL Client

You can use any SQL client of your choice, like Datagrip or DBeaver. The only requirements is to use Postres jdbc/odbc to connect to CRDB cluster.  
CockroackDB provides a shell client binary that you can install in Mac, Linux or Windows. Refer to the following [documentation](https://www.cockroachlabs.com/docs/stable/cockroach-sql-binary) to install CRDB sql client.

## Challenges

* [Performance Challenge](https://github.com/campossalex/CRDBGameGay/blob/main/performance_challenge.md)
* [Integration Challenge](https://github.com/campossalex/CRDBGameGay/blob/main/integration_challenge.md)
* [Resilience Challenge](https://github.com/campossalex/CRDBGameGay/blob/main/resilience_challenge.md)
* [Optimization Challenge](https://github.com/campossalex/CRDBGameGay/blob/main/optimization_challenge.md)
