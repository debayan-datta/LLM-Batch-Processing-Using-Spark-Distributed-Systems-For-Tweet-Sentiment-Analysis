
# LLM Batch Processing Using Spark Distributed Systems For Tweet Sentiment Analysis

The project focuses on implementing tweet sentiment analysis using Multi-Node Spark distributed system and Google's flan-t5-small model.

The workflow involves setting up the master node by configuring the Spark environment and accessing the Spark UI for monitoring. Worker nodes are similarly configured and connected to the master node. The sentiment analysis is executed using a Spark-submit command, with provisions for updating the Spark UI to monitor job status.




## Features

- Data Collection
- Multi-Node Spark Environment Setup
- Sentiment Analysis


## Requirements

- Ubuntu 22.04
- Multiple computers (though a single computer setup is also feasible)
- Spark, PySpark
- Transformers ()
## Data Collection

1. Sign up at https://apify.com/

2. Go to Store

Search for "Twitter"

Under "All pricing models" select "Pay per result"

    Select "Tweet Scraper V2 (Pay Per Result) - X / Twitter Scraper"

3. Clear "Start URLs".
Clear "Search Terms".

Under "Twitter handles" : 
            
    a. Clear all
	b. Put your desired twitter handle. (Eg: for Elon Musk, put 'elonmusk')
			  
Clear "Conversation IDs".

Under Maximum number of items on output : put 20 (Any)

Under Max tweets per query : put 20 (Any)

Clear everything under "Query Wizard".

Press Start

4.

Click Export (Bottom Left)

Select Format as CSV

Under Selected Fields select "text" only.

Press Download

#### Requires Data Cleaning
#### Remember to change this file path in my_spark_app.py
## Setup

#### You can check your ip address using 
    ip addr show
#### Start the master node using the following commands in your linux system

    cd $SPARK_HOME/conf
    cp spark-env.sh.template spark-env.sh
    export SPARK_MASTER_HOST=<give your own ip address>
    export SPARK_MASTER_PORT=7077 (Default port)
    export SPARK_WORKER_CORES=3   (Any)
    export SPARK_WORKER_MEMORY=3g  (Any)
#### To start your master node
    $SPARK_HOME/sbin/start-master.sh
#### To Check if Master Node Setup is Successful
    cat /opt/spark/logs/spark-hduser_-org.apache.spark.deploy.master.Master-1-bhaskara17.out
(Change Log File directory with your system log file directory obtained when starting master node)
#### Start your worker nodes with the following commands in your linux system
    cd $SPARK_HOME/conf
    cp spark-env.sh.template spark-env.sh
    export SPARK_WORKER_CORES=3
    export SPARK_WORKER_MEMORY=3g
    $SPARK_HOME/sbin/start-worker.sh spark://<master node ip>:7077
#### Use this to check you master node availability and connected workers nodes in your browser
    http://localhost:8080/
or

    http://<master node ip>:<port>

## Sentiment Analysis

#### Submit the file to the Master Node in the  spark cluster to run the application 
    spark-submit my_spark_app.py
#### If after submitting the .py file you get any jupyter directory error,then you can temporariry change that path variable
    unset PYSPARK_DRIVER_PYTHON


## Acknowledgements

 - [Distributed Llama 2 on CPUs](https://towardsdatascience.com/distributed-llama-2-on-cpus-via-llama-cpp-pyspark-65736e9f466d)
 - [Large Models Meet Big Data: Spark and LLMs in Harmony](https://towardsdatascience.com/large-models-meet-big-data-spark-and-llms-in-harmony-5e2976b69b62)
 - [Pritam Taldhi Github](https://github.com/Taldhi/Spark-ML-with-distributive-computing)
