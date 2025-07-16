## 

1.  How to load data into spark
    

\->Using Spark Dataframe API

2.  How to Query data in spark
    

\-> Using Spark SQL

*   Databases are most popular and widely used data processing platforms , Databases offers - Tables & SQL 
    
*   Table contains Schema (list of columns) & Data 
    
*   Metadata LAyer contains info. About table | Logical Layer Provides us the table data | Physical LAyer Stores file in Hard disk
    

Spark Offers 2 ways of data processing : 

1.  Spark Database and SQL
    
2.  Spark Dataframe & API
    

*   Spark data is internally stored as a files and these files and spark gives you flexibility  to choose file format.
    
*   Spark Storage Layers supports distributed storage such as Amazon S3,GCS,HDFS,ADLS etc.
    
*   Unlike SQL Table, Spark dataframe is runtime and temporary object, while TABLE remains saved in Catalog/databases
    
*   We create a table then load data into it, so data must be align with schema otherwise will give error, BUT in case of dataframe, we give schema while loading/creating dataframe.
    
*   So Spark will read the data from file and apply schema at the time of reading , then will create the dataframe using schema and load the data.
    
*   Dataframe can be always loaded with data while Table can be Empty.(But we can create empty dataframe as well manually)
    
*   Both are structurally same, so you can convert the dataframe into table or vice versa
    

## Spark Table VS Spark Dataframe:

## 

| Spark Table | Spark Dataframe |
| --- | --- |
| Table stores schema info. In metadata store | Dataframe stores schema in runtime Catalog |
| Table & Metadata are persistent objects,and visible across applications | Dataframe and Catalog are runtime objects and live only during the application runtime.Dataframe is visible to your applications only. |
| We create table with predefined table schema | Dataframe supports schema-on-read |
| Table supports SQL expressions and does not supports API | Dataframe offer APIs and does not supports SQL Expressions (we can use spark.sql to run SQL queries) |

## Creating Spark Dataframe: 

## 

Data Set : Fire Department Calls for Service 

Location: /databricks-datasets/learning-spark-v2/sf-fire/sf-fire-calls.csv

(Databricks have this dataset in community edition for users )

What are the requirements?:

1.Load the given data file and create spark dataframe.

2\. Use the spark dataframe to answer the following questions:

1.  How many distinct types of calls were made to the fire department?
    
2.  What are the distinct types of calls made to the fire department?
    
3.  Find out all responses or delayed times greater than 5 minutes?
    
4.  What were the most common call types?
    
5.  What zip codes accounted for the most common calls?
    
6.  What San Francisco neighbourhoods are in the zip codes 94102 , 94103?
    
7.  What was the sum of all calls ,average , min and max of the call response times?
    
8.  How many distinct years of data are in CSV file?
    
9.  What week of the Year in 2018 had the most fire calls?
    
10.  What neighbourhoods in San Francisco had the worst response time in 2018?
    

### Create dataframe to read the csv File:

## 

fire\_df = spark.read.format(“csv”) \\

               .option(“header”,”true”) \\

               .option(“inferSchema” ,”true”) \\

               .load(“/databricks-datasets/learning-spark-v2/sf-fire/sf-fire-calls.csv”)

This is a standard code for creating a spark dataframe.

→ spark : session object, entry point for spark programming APIs

Every spark program starts with the spark session bcoz spark APIs are available to use via session objects.

→ spark session object have many attributes/methods : read,builder,catalog,range,sql,stop,readStream,conf,etc.

→ We have used the ‘read’ attribute in our code.

→ format,optrions,load are the methods of reader

→ .format(“csv”) means I am telling the dataframe reader that my file is in the ‘csv’ format.

→ my csv file have header row (header-true)

→I am also saying that a dataframe reader should infer the schema from the file itself.

→dataframe reader will format the options to read the file.

Accessing Spark Documenations: You can access spark python documentation ; go to spark documnenation website -> API Docs -> Python → API Reference

( you will get all the details and parameters list can pass to each method)

→ We can also load the csv data using the csv() method.

Fire\_df = spark.read.csv(“/databricks-datasets/learning-spark-v2/sf-fire/sf-fire-calls.csv”,header = “true”,inferSchema = “true”)

→ The difference between above two codes is nothing but  here we are using shortcut

→ However, the Long code along with the format(), option() methods is recommended as  it can be used for other file types as well.

→ But we should know the shortcut methods available to read the data from different file types. We have 6 different shortcut methods to read data from : 

*   DataFrameReader.csv
    
*   DataFrameReader.json
    
*   DataFrameReader.parquet
    
*   DataFrameRaeder.orc
    
*   DataFrameReader.jdbc
    
*   DataFrameReader.table
    

→ Spark supports many datasources such as XML, other than listed above.

## Pyspark create table/view from Dataframe:

## 

1.  df.show(10) : shows first 10 records , but not in readable or clean manner, you can use display() function instead if you see that data in tabular format in a good way.
    
2.  display(df) : function is not part of Apache Spark, it is an optional tool available / provided by databricks, it shows the contents of the df.in tabular format.
    
3.  df.createGlobalTempView(“fire\_service\_calls\_v”): to create a global temp view of dataframe, which is similar to the table, we can write SQL expressions on tempview.
    

→ SELECT \* FROM global\_temp.fire\_service\_calls\_v ;

→ global\_temp is a hidden database , and all global temp tables are created inside this global\_temp database.

## Creating Spark Tables:

## 

CREATE DATABASE IF NOT EXISTS demo\_adb

→ Now you should see two databases in ‘Catalog’ ie. default & demo\_adb

→ CREATE TABLE IF NOT EXISTS demo\_adb.fire\_service\_call ( col1 integer,name string) USING parquet

→ Every database table internally stored data in a file.; hence we have given here as to create a table using a parquet file format.

→ And we can insert records into a table created using ‘INSERT INTO’ using SQL.

→ We do not have delete capability in Apache spark, we can truncate the table

→ However databricks provide the DELETE on tables but we are looking into Spark .

→ INSERT INTO demo\_adb.fire\_service\_call 

SELECT \* FROM global\_temp.fire\_service\_calls\_v

→ Means in this way we can insert from temp view into our table using SQL.

→Spark works in 3 Layers- Metadata Layer, Compute LAyer,and Storage Layer.When any of these layer have issue then it will throw error while running your code.

→As Databricks Community Edition have some limitations, after 2 hours of inactivity , daabricks will automatically terminate your cluster. 

→ Once the Cluster gets terminated, it deletes 1\. Cluster VM 2.Spark Metadata Store

→So you will lose your database you created ie. demo\_adb;This problem does not persists on Licensed Databricks.

→Although Databricks Community edition cleans up the luster VM & Metadata store, BUT it does not cleans up the directories and files.

→ Directories are created in an External Distributed Storage; and hence the files are saved in these directories o external storage; and External storage is not the part of the cluster.

→So If we try to create the same table again using parquet with the same location , we might get error, ‘AnalysisExceptio’ : CAnnot create managed table <table\_name> .The associated location (dbfs:/user/../fire\_service\_call) already exists.

→ Because, Databricks did not cleaned the directory and data files.

→ To solve this issue, you can clean up the directory manually.

→ %fs rn -r /../warehouse/demo\_adb.db (the directory name you will get from error as well)

→ Do not delete warehouse directory bcoz it is the default location for all the spark databases.

→You also add DROP Table , and database(DROP VIEW IF EXISTS demo\_adb)

## Working With Spark SQL:

## 

→ As we know that we can run SQL queries on the table we have created, we can find the answers of above questions using SQL queries.

## DataFrame Transformation & Actions:

## 

→ Go to Pyspark documentation, API References and go to latest documentation, see pyspark.sql.Dataframe , there you will see all the objects of spark dataframe/ list of methods and also the list of attributes.

→ These are all methods but we can classify them into 3 logical groups 

1.  Actions
    
2.  Transformations
    
3.  Functions/Methods
    

→ Actions : triggers the spark job and returns to the Spark driver. Ie. Actions are Dataframe operations that kick off a Spark Job execution and return to the Spark Driver.

→ Transformations: Spark Dataframe Transformation produces a newly transformed Dataframe. ; Transformations are different from actions , they do not kick off spark jobs and they do not return to the driver.; They simply create a new dataframe and return it.

→Functions / Methods : These are Dataframe methods or functions which are not categorized into Actions and Transformations.

### List of Spark Actions | Transformations | Functions - Methods :

## 

| Actions | Transformations | Functions/Methods |
| --- | --- | --- |
| collect | agg | approxQuantile |
| count | alias | cache |
| describe | coalesce | checkpoint |
| first | colRegex | createGlobalTempView |
| foreach | crsossJoin | createOrReplaceGlobaltempView |
| foreachPartition | crosstab | createOrReplaceTempView |
| head | cube | createTempView |
| show | distinct | explain |
| summary | drop | hint |
| tail | drop_duplicates | inputFiles |
| take | dropDuplicates | isLocal |
| toLocalIterator | dropna | localCheckpoint |
|  | exceptAll | persist |
|  | filter | printSchema |
|  | groupby | registertempTable |
|  | intintersect | toDF |
|  | ersectAll | toJSON |
|  | join | unpersist |
|  | limit | writeTo |
|  | orderBy | withWatermark |
|  | randomSplit |  |
|  | repartition |  |
|  | repartitionByRange |  |
|  | rollup |  |
|  | sample |  |
|  | sampleBy |  |
|  | select |  |
|  | selectExpr |  |
|  | sort |  |
|  | sortWithinPartitions |  |
|  | subtract |  |
|  | transform |  |
|  | union |  |
|  | unionAll |  |
|  | unionByName |  |
|  | where |  |
|  | withColumn |  |
|  | withColumnRenamed |  |

→ There are also 10 more Functions/Methods available but are available in python and not in other languages hence excluded from above list and are also don't bening used frequently.

## Applying Transformations:

## 

→ Will apply transformations / function in pyspark which we did in SQL query to find the ans. Of given questions.

→ display(df) : Dataframe column names are not standardised,column names have spaces in them; Date fields are of string types. 

→ withColumnRenamed : to Rename columns 

→renamed\_fire\_df = raw\_df \\

                                  .withColumnRenamed(“Call Number”,”CallNumber”)  

→(old col name , New Col Name)

→ We can chain the withColumnRenamed  to rename the other columns

→renamed\_fire\_df = raw\_df \\

                                  .withColumnRenamed(“Call Number”,”CallNumber”) \\

                                  .withColumnRenamed(“Unit ID”,”UnitID”)

→ Writing a PySpark code is nothing but the 2 things: 

1.  Read your Raw Data into Dataframe
    
2.  Transform your raw dataframe and create a new transformed Dataframe.
    

→ Keep the following things in Mind:

1.  You can create a chain of Spark Transformation methods one after the other.
    
2.  Spark transformation returns a new dataframe after transforming the old dataframe.
    
3.  Spark dataframe is immutable.(you can't change or update existing dataframe, instead you can transform an existing dataframe to create a new dataframe.)
    
4.  Spark DataFrame transformation produces a newly transformed dataframe.
    

→ So we have resolved the ‘COlumn name ‘ issue now all columns in our dataframe are in standard format(‘without space’)   BUT we have other issue still exists ie. Date columns are in string format.

→ We can print the schema using the printSchema() utility.

→ renamed\_fire\_df.printSchema() 

→ we can see ‘CallDate,WatchDate etc columns in string data type.If we didn't change it to date type then we need to cast it in date format every time whenever we use these date columns. 

→ ‘withColumn‘ is a commonly used transformation , it can transform one column into another column.

→ fire\_df = renamed\_fire\_df \\ 

                   .withColumn(“callDate” , to\_date(“CallDate”,”MM/dd/yyyy”))

→ here ‘withColumn() takes two parameters - columnname, & logic to transform the column.

→ We should import the function form pyspark package 

→ from pyspark.sql .functions import\*

→In this way we can chain up the same function ‘withCOlumn’ in chain to transform the other columns.

→ fire\_df = renamed\_fire\_df \\ 

                   .withColumn(“callDate” , to\_date(“CallDate”,”MM/dd/yyyy”)).withColumn(“AvailableDtm” , to\_timestamp(“AvailableDtm” , “MM/dd/yyyy hh:mm:ss a”)).withColumn(“Delay”,round(“Delay”,2))

→ So what we learnt is -

1.  Column Transformation Methods : WithColumnRenamed()  , withColumn()
    
2.  Utility Method : printSchema()
    

## Querying Spark Dataframe : 

## → we can cache dataframe as fire\_df.cache() 

→ To answer the question we saw in the previous video and solved using SQL query, we have 2 approaches 1. SQL Approach 2.Data Frame Transformation Approach.

→ 1. SQL Approach =>  fire\_df.createOrReplaceTemView(“fire\_service\_calls\_view”)

ql\_sql\_df=spark.sql(“ “ “ <sql Query> “ “ “)   

display(ql\_sql\_df)

→ 2.Dataframe Transformation Approach => 

As per the SQL query for Q1, we have to 

1.  Filter the records and take only those where CallType is not null.
    
2.  Select the CallType column 
    
3.  Take only Distinct Call Types
    
4.  Show the Count
    

We can do this in chain of 3 methods:

q1\_df = fire\_df.where(“CallType is not null”) \\

                       .select(“callType”) \\

                       .distinct()

print(q1\_df.count())

→ So in this code , we learnt 3 Transformations:

1.where() 

2.select()

3.distinct()

 and 1 Action:

1.count()

→we can also use these transformations in separate data frames one by one but that is not readable and not the best practice as well.

→ Actions : Actions are DataFrame operations that kick off Spark Job Execution and return to the Spark Driver.

→ ie. Action does not return a dataFrame , it returns the result to the driver.

eg:.count()

→ It is best practice to keep an ‘Action’ in a separate line , we can chain the action in the end,we cannot chain anything after we call an Action.

< to solve remaining questions using dataframe approach> 

## More Data Frame Transformations:

## Actions: Actions are dataframe operations that kick off a spark job , execute and return to the spark driver.

*   For eg: df.show() , display(df)
    

Q2) What were distinct types of calls made to the fire Departmnet?

→ SELECT DISTINCT calltype AS distinct\_calltypes

     FROM fire\_service\_call\_table

     WHERE calltype is NOT NULL

q2\_df = fire\_df.where(“calltype is not NULL”) \\

                       .select(expr(“calltype as distinct\_call\_type”)) \\

                       .distinct()

q2\_df.show()    —prefer using actions on new line.

Note: display() function is not part of Apache Spark, it is an utility function provided by datarbrikcs.

\-Display() function formats the result while Show() displays the output in the plain text format.

Q3) Find out all responses for delayed times greater than 5 mins?

→ SELECT callnumber , delay 

FROM fire\_serivce\_calls\_tbl

WHERE delay > 5

fire\_df.where(“delay > 5”) \\

          .select(“callnumber”,”delay”) \\

          .show()

Note: We can chain ‘Action’ to the data frame transformations, BUT we can chain only 1 action at a time in a dataframe. 

\-Once you added an action to the dataframe , you cannot add more transformations to it because the action does not return the data frame anymore.

Q4) What were the most common call types?

→ SELECT caltype , COUNT(\*) AS count

FROM fire\_service\_call\_tbl

WHERE calltype IS NOT NULL

GROUP BY calltype

ORDER BY count DESC 

Note: As we saw earlier, count() is an action and we know action does not return a dataframe. But if we use ‘count()’ after groupBy() transformation , then it is transformation on grouped data & not the count().

\- Dataframe.count() → Action

\- GroupedData.count() → Transformation

fire\_df.select(“calltype”) \\

          .where(“calltype is not null”) \\

          .groupBy(“calltype”) \\

          .count() \\

          .orderBy(“count”,ascending = False) \\

          .show() 

\*\* Need to solve remaining questions by our own using pyspark
