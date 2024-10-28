# Integration Challange

Goal: stream data changes to a Kafka topic.  

Kafka cluster information:  

- Control Center web console: [Confluent Control Center](http://18.216.213.38:9021/clusters/cJ2ocmjVSFOA5y71ezdpIw/overview)  
  Once in Control Center, click `Topics` on the left-hand side menu.  
- Kafka Ip Address Listerner: 18.216.213.38  
- Kafka Port: 9092

Table `movr.vehicle_location_histories`. This table is already create from the previous challenge.  

💡 Use the following tips to send data to Kafka.  

Make sure rangee feed feature is enable in your cluster.  

```
SET CLUSTER SETTING kv.rangefeed.enabled = true;
```

CREATE a change feed.  

```
CREATE CHANGEFEED FOR TABLE <ddbb.table> INTO 'kafka://<kafka_connection>?topic_name=<topic_name>';
```
Once data is streamed to Kafka, refresh in the `Topic` page in Control Center to see your topic name. To list the messages, click the topic and go to the `Message`.

Check the CHANGE FEED job status.  

```
SHOW CHANGEFEED JOB <job_id>;
```
