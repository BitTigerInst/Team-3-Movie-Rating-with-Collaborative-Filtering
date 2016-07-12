Update time: 2016/06/27
This is the notebook for the BitTiger project. I will record all steps, give references, and it will be beneficial to people who are interested in this project.

# Set up environment
In this project, we use Spark and Scala as technical stack. In other to fast deployment and easy to use, we use [sequenceiq](https://github.com/sequenceiq/docker-spark)'s docker. The versions are Hadoop 2.6.0 and Apache Spark v1.6.0 on Centos. Here is the setting steps:

## Pull the image from Docker Repository
```
docker pull sequenceiq/spark:1.6.0
```

## Building the image
```
docker build --rm -t sequenceiq/spark:1.6.0 .
```

## Running the image

* if using boot2docker make sure your VM has more than 2GB memory
* in your /etc/hosts file add $(boot2docker ip) as host 'sandbox' to make it easier to access your sandbox UI
* open yarn UI ports when running container
```
docker run -it -p 8088:8088 -p 8042:8042 -p 4040:4040 -h sandbox sequenceiq/spark:1.6.0 bash
```
or
```
docker run -d -h sandbox sequenceiq/spark:1.6.0 -d
```

## Testing

There are two deploy modes that can be used to launch Spark applications on YARN. We mainly use first mode.

### YARN-client mode

In yarn-client mode, the driver runs in the client process, and the application master is only used for requesting resources from YARN.

```
# run the spark shell
spark-shell \
--master yarn-client \
--driver-memory 1g \
--executor-memory 1g \
--executor-cores 1

# execute the the following command which should return 1000
scala> sc.parallelize(1 to 1000).count()
```
### YARN-cluster mode

In yarn-cluster mode, the Spark driver runs inside an application master process which is managed by YARN on the cluster, and the client can go away after initiating the application.

Estimating Pi (yarn-cluster mode):

```
# execute the the following command which should write the "Pi is roughly 3.1418" into the logs
# note you must specify --files argument in cluster mode to enable metrics
spark-submit \
--class org.apache.spark.examples.SparkPi \
--files $SPARK_HOME/conf/metrics.properties \
--master yarn-cluster \
--driver-memory 1g \
--executor-memory 1g \
--executor-cores 1 \
$SPARK_HOME/lib/spark-examples-1.6.0-hadoop2.6.0.jar
```

Estimating Pi (yarn-client mode):

```
# execute the the following command which should print the "Pi is roughly 3.1418" to the screen
spark-submit \
--class org.apache.spark.examples.SparkPi \
--master yarn-client \
--driver-memory 1g \
--executor-memory 1g \
--executor-cores 1 \
$SPARK_HOME/lib/spark-examples-1.6.0-hadoop2.6.0.jar
```

### Submitting from the outside of the container
To use Spark from outside of the container it is necessary to set the YARN_CONF_DIR environment variable to directory with a configuration appropriate for the docker. The repository contains such configuration in the yarn-remote-client directory.

```
export YARN_CONF_DIR="`pwd`/yarn-remote-client"
```

Docker's HDFS can be accessed only by root. When submitting Spark applications from outside of the cluster, and from a user different than root, it is necessary to configure the HADOOP_USER_NAME variable so that root user is used.

```
export HADOOP_USER_NAME=root
```

# datasets


