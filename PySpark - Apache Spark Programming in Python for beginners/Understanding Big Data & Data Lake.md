## What is Big Data and How it started?

*   Data processing is one of the critical business requirements
    
*   We used RDBMS for decades to develop data processing applications
    
*   The advent of internet started putting following data processing challenges:
    

*   We started collecting variety of data: 
    

*   Structured 
    
*   Semi-structured
    
*    Unstructured
    

*   Business Started collecting high Data Volumes.
    
*   Need to collect and process data at high velocity.
    

*   The new challenge is popularly known as the Big Data Problem.
    
*   The big data problem was defined using 3Vs of Big data - Variety , Volume , and Velocity.
    
*   RDBMS failed to handle the Big Data Problem.
    
*   Industry needed a new approach or platform to handle the Big Data problem.
    

  

Scientists and Engineers came up with new approaches to solve the big data problem,

However we sort 2 categories:

  

*   Monolithic Approach
    
*   Distributed Approach
    

  

### Monolithic Approach:

  

*   This approach designs one large and robust system that handles all the requirements.
    
*   Teradata and Exadata are examples.
    
*   These 2 systems support only 2 - structured and semistructured data , So we cannot call them as big data systems but they are designed using a monolithic approach.
    

  

### Distributed Approach:

  

*   In this approach , we take many smaller systems and bring them together to solve a bigger problem
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe98tuxg2sbQz8l1wl5ZFJGWGDeduiiins1WO6ynN7-rU7ltFDAzSzIwhuaMel6IOOR5PZkdRkNko0vN0wdDvRBnNjr41vI2qBNvHeqOZlqwdua22LoPyF4iFwpNg-NtQ?key=zIq_3dhjyE7hjZbanHRPXd4d)

  
  

| Criteria | Monolithic Approach | Distributed Approach |
| --- | --- | --- |
| Scalability | vertical | Horizontal |
| Fault Tolerance & High Availability | Primary/Secondary | Multifold |
| Cost-Effectiveness | Expensive | Economical |

  
  

*   Hence Hadoop came as a distributed Big Data Processing Platform
    
*   It was designed and built in layers.
    
*   YARN : Distributed cluster formation | Cluster Operating System
    
*   HDFS : Distributed storage
    
*   Map/Reduce : Distributed Computing (Distributed programming using java , python etc)
    
*   Hadoop allowed us to use a set of / cluster of computers as a single Large Machine.
    
*   Hadoop allows us to store data.
    
*   These 3 are the main core services provided by hadoop , but after that hadoop community develop other tools and platform on top of the hadoop like  hive database, hbase database, pig scripting language
    

  

### Database & Hadoop : 

  

| Database | Hadoop |
| --- | --- |
| Data Storage | Data Storage |
| SQL Query language | Hive SQL query language |
| Scripting language | Pig Scripting Language |
| MYSql,Oracle,SQL Server | python,sql,java |

  

Hadoop supported most of the RDBMS capabilities and also supported Big data capabilities.

  

## Hadoop Architecture , History , Evolution:

### YARN - Yet Another Resource Manager:

*   Hadoop CLuster Operating System 
    
*   Popularly known as Hadoop cluster resource manager
    
*   Has three main components : 
    
*   RM - Resource Manager
    
*    NM - Node Manager
    
*    AM Application Master
    
*   Installing and configuring a Hadoop cluster is as simple as installing software on your computer.
    
*   Hadoop uses Master-Slave Architecture,So one of the machines from the cluster will become a master and the remaining will work/act as a worker node.
    
*   The Node manager will send the regular status report to the resource manager(Master).
    
*   We created an hadoop cluster so that we can run big data applications
    
*   To run application in Application MAster (in Worker node) , Master node requests worker\_node to run the application
    
*   Your application runs inside the AM container.
    
*   If I submit another application, the resource manager will again do the same process.
    
*   Each application in YARN runs inside a different AM container.
    

  
  

### HDFS : Hadoop Distributed File System:

  

*   Distributed storage on hadoop cluster
    
*   Has two main components 
    

*   NN - Name Node
    
*   DN - Data Node
    

*   It allows you to save and retrieve data files in a cluster.
    
*   As we know Hadoop works on master - slave architecture., So Hadoop will install NN service on master , and DN service will run  on slave (worker) nodes.
    
*   The NN with DN forms the HDFS.
    
*   Let's assume you want to copy large data files on your cluster,So you will initiate the file copy command. The file copy request will go to the name node (NN).
    
*   The NN will redirect the file copy command to one or more DN .File copy command will split the file into smaller parts(each part known as block). 
    
*   NAme node facilitates this process , and keeps track of all the file metadata. 
    
*   What metadata? : file name,directory location , file size ,file blocks ,block Id,block sequence , block location.
    
*   Now, consider for file read. The NN contains all the information about the file , how and where it splitted and stored on blocks in DNs.
    
*   NN will redirect the read operation to the target data nodes.
    
*   Read Api will receive data blocks from DN and reassemble the file using the data received from DNs. 
    

  

### Map/Reduce : 

*   Hadoop Map Reduce Framework
    
*   Map Reduce is : 
    
*   Programming Model : It is a technique or way of solving problems
    
*   Programming Framework : It is a set of APIs& Services that allows you to apply the map/reduce programming model.
    

  
  

### Hive Capabilities : 

1.  Create : 
    

1.  Databases 
    
2.  Tables
    
3.  Views
    

3.  Run SQL Queries
    
4.  Hadoop as a platform and Hive as a database became very popular.
    
5.  Still Hadoop was having some disadvantages : 
    

1.  Performance
    
2.  Ease Of Development
    
3.  Language Support
    
4.  Storage
    
5.  Resource Management
    

7.  Hence Apache spark came into picture with above issues as improvement over the mapreduce.
    

  

## Advantages (of Apache Spark) Over Hadoop:

*   Performance : 
    

*   10 to 100 times faster than Hadoop Map/Reduce
    

*   Ease of development :
    

*    Spark SQL
    
*   High Performance SQL engine
    
*   Composable Function API
    

*   Language Support: 
    

*   Java , Scala ,Python and R
    

*   Storage:
    

*   HDFS Storage
    
*   Cloud Storage
    

*   Resource Management:
    

*   YARN , Mesos,Kubernetes 
    

  
  

### Apache Spark Runs in two setups:

1.  With Hadoop (Data Lake)
    
2.  Without Hadoop (Lakehouse)
    

  

## What is Data Lake and How does it work?:

*   It all started with google they finding the solution to store files using GFS → HDFS
    
*   The open source community created a similar solution called HDFS; it allowed us to form a cluster of computers.
    
*   We also got the Map-reduce framework
    
*   Key missing features from Data Lake in earlier days : 
    
*   Transaction & Consistency
    
*   Reporting Performance
    
*   There were other issues which Data Lake could not support but above mentioned are the main issues.
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdKHgiddL8Ux7RY5sRtijVhQYa5vLxA1E91a8QMptdrU7Wm7iyd3jHvZl82-JESpZgrKQzqPQlsrKqQGqlK0q1coJ3Iap3HfdzFLXpbjJowNMQGBaF0uaNv5liQwMy8f1aadHaUaA?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   So we started to adopt different architecture for implementing a data lake.
    
*   We started to integrate relational databases and data warehouses for reporting and BI purposes.
    
*   So basically, we collected data in Data Lake Storage; Processed it using Apache Spark; and Export the result in Data Warehouse.
    
*   Finally, we connected the Reporting and BI with the Data Warehouse.
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfGdKgeON-bPue3pt9XANutCOm1XS7VmDclsyw2F3BpMYfa70eOChBhbP30M7uQj9n8q9ClRxL_ISGtrwnxADVWgJoOtJUCtP5Xg7hDVMQHy3JAJTqhQ32XV7OKuYKBjGBZBToQzA?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf-Vws7XzuK0oIY_QRIqqoPObQSc5ioLIRznl8nKBY4GsRyyupGFFW3SOpHfOT2CK4coqfwyAec1gbKBUg2uP1mA-Ww_kX1ObrxNgm3FtirhRWaBFkczI9rbRUTSkPifTKNXlzZ-Q?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   Next Layer is the processing layer, where all the computation is going to happen.
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXduxQ3HvagmZEbPsfgDpPVP3vxn1DlPMbSIjCtDB2_4lqfMeqPffgEZLN-7q1uTx0UAdQL1tlQDwcyefk8VTL6waOiaOlFIuHIXocRIf-zpF50b1DAZq_K4WD_VdINdKyOeVIjqNg?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   The Apache Spark falls in this place.
    
*   The last and the most critical capability of the data lake is to allow you to consume the data from the data lake.You can think of the data lake as a repository of Raw and Processed data.
    
*   Now the consumption is to put the data for real life usage.
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfxo6urfaKUYpa1zU6WotKbGy9VAkn1k-8ZPJyqXoc5tHgoNrVvh91PYbDcBRIAsLYNvsbxDa6zhehBic2MOLV3qOzOpOqGFy24KsLo0wjtX3N3xv9xd3KaIlzCUIK_ELANk1cxDA?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfKVqiAzvbuC8U4SxwpU8iXnXW7WkkrZ2uGPg4qYSOgvhKh95Ty8K6FLPvJQypyaaNqCBQClxhon5dbLcCzHgykIRQinnLLMvRxHn9v_EdGrBFfjLiI57-fiAYLYf1shTuznJLLWA?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   This is about the data lake at a higher level.
    
*   However, the Data Lake platform is much more complicated at the Whole.
    

  

## Introducing Apache Spark and Databricks Cloud:

  

*   We have seen the Data Lake as a Modern Data Lake Platform, and you have now understood the idea of distributed computing.
    
*   We also know that Apache Spark is the most popular framework in a Data Lake.
    
*   Lets get some deeper into Apache Spark, and understand Spark as Unified Data Analytics and Processing Platform.
    
*   Apache Spark is the distributed processing framework,The diagram below shows the Spark Ecosystem.
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXciqbdiibCJBoNoHSTVVy51-YEdzMv_TMSIjKhl1Z200Ney6q5dLlWhl8XCRtUEZRm74EXGCQ_L43rxvrpV_Lk7pWPRsTH4xXcbuF5kmzGdsUPmZYvcA0AiuLEA0yEUp0IRtjcNfQ?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   The Spark Ecosystem is designed in 2 layers, One is Spark Core Layer , and the other layer is set of libraries, DSS and APIs
    
*   These 2 things together make the spark ecosystem.
    
*   Spark Core layer itself have 2 parts: Spark Engine(Distributed computing Engine)  & Set of core APIs
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf5EIYD51VGJGXuuFkaNVX06nu2b3nEC1_m4-tWMXsy_RAEt6dK8fOudqWDBOaNaUbIq2HQp7ZfOYReVtBHXZc5NdzHwhf9jUnA4yDYl4PVocMlCSq21PzTnQcHIp48rmeimef9Bw?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   And this whole thing runs on a cluster of computers to offer you distributed processing.
    
*   However , the spark does not manage the cluster;it only gives you a data processing framework , So we are going to need a cluster manager(Resource Manager OR Container Orchestrator)
    
*   Spark was initially based on hadoop Map/reduce , and it was adopted in the Hadoop Platform, So Hadoop YARN resource manager is the most commonly used Cluster Manager in Spark.
    
*   However, you have other options: YARN | Kubernetes | Mesos
    
*   Spark does not come up with an inbuilt storage system and it allows you to process the data stored in various distributed storage systems.
    
*   Most Popular and commonly used storage systems are : HDFS | S3 | Azure Blob | GCS | CFS (Cassandra File System)
    
*   Inshort  , Apache Spark does not provide us with the Cluster management and storage management; All you can do with Apache Spark is to run your Data Processing Workload and that part is managed by the Spark COmpute Engine.
    
*   All you need is to submit data processing jobs to spark and spark engine will take care of everything else.
    

  

*   The next layer is again the Spark core layer which contains APIs like JAva,R ,Scala,Python etc. that we used to write DAta Processing logic in the initial days of Apache Spark.
    
*   However, these APIs are based on Resilient Distributed Datasets(RDDs)
    
*   And people found them tricky to learn and use in the day to day Data Processing work ; Some people still use them today.
    
*   But these APIs are most complicated to work on Apache Spark ; They also lag some performance optimization features and now spark creators are recommending them to avoid use as much as possible.
    
*   However, these APIs can provide you with the highest level of flexibility to solve some Complex Data Processing Problems.
    
*    The topmost layer is again the set of APIs which can be used for data scientist ML purposes.
    

  
  

### Why Apache Spark is best?:

*   Abstraction
    
*   Unified Platform
    
*   Ease of Use
    

  

Apache Spark is an open Source Project,The original creators of Apache Spark donated it to the Apache Foundation and made it an open source project. The same team formed a company and a commercial product around the Apache Spark.The company and the product both named databricks.

  

So what do they offer over and above the apache spark?: 

  

### Databricks : 

*   Spark on the cloud Platform : Databricks brings spark to the cloud platform.
    
*   Spark Cluster Management : Databricks allows you to run a cluster ; it allows you to install , configure all the dependent and run time libraries on all the nodes to your spark application.
    
*   Notebooks & Workspace: as good as IDE for spark development, can share with colleagues. CAn configure Git repo.
    
*   Administration Controls 
    
*   Optimized Spark : Provides us the optimized and tuned version of Apache Spark.Databricks Spark runtime is 5 times faster than the standard Apache spark runtime.
    
*   Databases / Tables & Catlog: Provides integrated Hive metastore allowing us to create databases,tables,views etc.using spark SQL.
    
*   Databricks SQL Analytics: On top of this, Databricks also offers an Advanced SQL Query Engine called : Photon - which allows us to gain data warehouse grade performance using SQL query and Dashboard on top of the Data Lake Infrastructure.
    
*   Delta Lake Integration
    
*   ML Flow
    
*   Industry Vertical Accelerators.
    

  

Even if the Apache spark is at the core, Databricks has a lot to offer on top of the Apache Spark.Most importantly,Databricks make spark implementation super easy for all three major cloud platforms - GCP , Azur,AWS.
