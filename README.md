This Knime workflow represents a pipeline that receives information from kafka's one topic, performs operation on it and publishes it back to a second topic on kafka.

This workflow consumes transaction records for each customer ID in JSON format from kafka. For the customer ID field in a record, the workflow fetches extra customer informaton from an already existing table and appends the information to the processing record. Also, the same is done for each product number in the record. Once, complete information is available in a single table, the workflow aggregates the data to calculate all the products bought by a single customer and the total amount spent by him. This aggregated information is passed back to kafka on topic "customer_transactions".

To run this worfklow :
1. Start Kafka cluster on your local system
2. Create a topic "transactions" and publish JSON records of the following form to it:
{"OrderNumber" : 23893756,"Date" : "8-28-2015","CustomerID" : "69-695-442-229","ProductNr" : "I-163-2017"}.
3. Once that is done, edit kafka consumer node to edit the stop criteria and change the time stamp value.
4. Now, run the workflow
5. Once the workflow is completed, run a kafka consumer on your local system and consume from the topic "customer_transactions". The processed records with aggregated information should be available on the new topic.

Kafka producer and consumer nodes in knime have an extra set of additional configurations that map to the options available for kafka producer and consumer respectively.

To use a knime workflow on knime analytics platform
1. Clone the repo
2. Zip the folder created
3. On knime analytics platform, go to file > Import workflow
4. Here, select the zip folder. The data files, along with the workflow will be imported in the Analytics Platform. 
