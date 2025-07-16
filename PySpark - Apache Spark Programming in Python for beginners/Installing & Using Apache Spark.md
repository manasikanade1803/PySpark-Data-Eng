## 

Spark projects are developed in 2 kinds of  environments:

1.Cloud Platforms

2.On-Premise Platforms

  
  

And we have 2 standard methods : 

1.  Python IDE
    
2.  Notebook 
    

If your project is going in the cloud then you should prefer notebook; and on-premise projects prefer to use IDE.Or any of the method irrespective of env.

  

# Databricks Workspace:

## 

*   Workspace allows you to create project directories.
    
*   By default 2 Directores are already created : Shared & Users
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd1gl_hdKpKtZTXWXCnhVw85FdRw28bA5sNrsgPgCOQm5hSXD9m47-ej-Oz1ygRQbFTRXdc3erHJMuqxDJQQkCVKcYXOy_1OztwLchTNV9esBKXqeTKgJn2Zqe-uzQmAKpdPrFJfA?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   Shared Directory is a shared location to share project files/code to other team members/users ; BUT you should have a multiuser environment ( which databricks community edition does not supports)
    
*   Databricks allows you to create a single node cluster created in  ‘COMunity Edition’ for free of cost; but you cant restart that cluster once terminated of inactivity.
    
*   To read a csv/json or any file using pyspark, you need a data file, because spark is a data processing framework which needs data, Databricks Community Edition allows you to upload the file to process it.
    
*   You get one free cluster and some free storage in the cloud for keeping your data layer to run,develop your code.
    
*   DBFS - (storage u get by databricks free community edition) it is Databricks File System, a wrapper around the cloud storge, behind this DBFS you have amazon S3,etc. Storage.
    
*   If DBFS is not seen in ‘Data’ tab then you must need to go to settings.
    
*   Go to Email icon in Databricks, click on settings, and ref below Screenshot:
    
*   ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf3Q5uepCsfMKnWWVO1-sa4kkHQvvfhTfn1JqmLOXGkRXojACxBshe5j_PHfFPoTQ8N5M9t8fDg5B-HnBqgx3ud3iTZ9122bbllPtj6-xnfJ09LrUQWblDdXvQ5SXwl7JlKSriR6Q?key=zIq_3dhjyE7hjZbanHRPXd4d)
    
*   By default ‘FileStore’ Directory is there .
    
*   You can create your own data directores
    
*   You cannot run any code without any Spark Cluster and Spark Runtime Environment.
