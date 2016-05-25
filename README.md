# Sparkling-Water-EMR 

Below are steps to set up [AWS EMR](https://aws.amazon.com/elasticmapreduce/) with [Sparkling Water](https://github.com/h2oai/sparkling-water)

# Setting up your EMR Cluster:

##Step 1
  - Set up AWS credentials
    - Go to [https://aws.amazon.com/](https://aws.amazon.com/) and click the link `Create an AWS Account`

##Step 2
  - Sign into your AWS Console and navigate to `EMR` under `Analytics`

##Step 3
  - Configure your EMR instance as follows:
    - Cluster name: 'MyCluster'
    - Leave `Logging` checked
    - Leave `S3 folder` as its default (can change if ou have a specific folder in mind)
    - Launch Mode should be set to `Cluster`
    - Vendor should be set to `Amazon`
    - Release should be set to latest
    - Applications should be `Spark: Spark 1.6.1 on Hadoop 2.7.2 YARN wih Ganglia 3.7.2`
    - Choose `Instance Type` and `Number of Instances` as you see fit
    - `Security and access` should be left as default, but choose an appropriate `EC2 key pair` (made when you set up an AWS account)
    - Click `Create Cluster`

## Now you have an AWS EMR cluster ready to go!

# Launch Sparkling Water from your new EMR cluster:

  - SSH into your new EMR cluster as follows:
    -  Navigate to `Master public DNS` and click on `SSH`, which will give you instructions on getting into the EMR master node
  - After you ssh into your cluster run the following to start up Sparkling Water (in Spark Shell):
      ```
      spark-shell --packages ai.h2o:sparkling-water-examples_2.10:1.6.3 --executor-memory=6g --driver-memory=6g
      ```
  - Now you should have a spark shell running. Next, run the following commands to set up Sparkling Water:
      ```
      import org.apache.spark.h2o._
      val hc = H2OContext.getOrCreate(sc)
      ```
  - Now you should see two URL's that point to H2O's flow interface. Please point to those in your browser to get access.
  
## Now you have an AWS EMR cluster running Sparkling Water!

  - Sparkling Water demos are also available here: [https://github.com/h2oai/sparkling-water/tree/master/examples](https://github.com/h2oai/sparkling-water/tree/master/examples)
  - To run these demos you must copy them into your master EMR node.
