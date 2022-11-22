# Data Analysis using Spark on zOS and Jupyter Notebooks

[Apache Spark](https://spark.apache.org/) is an open-source cluster-computing framework. Spark runs on Hadoop, Mesos, standalone, or in the cloud. It can access diverse data sources including HDFS, Cassandra, HBase, and S3. And you can use it interactively from the Scala, Python and R shells. You can run Spark using its standalone cluster mode, on an IaaS, on Hadoop YARN, or on container orchestrators like Apache Mesos. 

[z/OS](https://en.wikipedia.org/wiki/Z/OS) is an extremely scalable and secure high-performance operating system based on the 64-bit z/Architecture. z/OS is highly reliable for running mission-critical applications, and the operating system supports Web- and Java-based applications.

In this jurney we demonstrate running an analytics application using Spark on z/OS. [Apache Spark on z/OS](https://www-03.ibm.com/systems/z/os/zos/apache-spark.html) is in-place, optimized abstraction and real-time analysis of structured and unstructured enterprise data which is powered by [z Systems Community Cloud](https://zcloud.marist.edu). 

z/OS Platform for Apache Spark includes a supported version of Apache Spark open source capabilities consisting of the ApacheSpark core, Spark SQL, Spark Streaming, Machine Learning Library (MLib) and Graphx.It also includes optimized data access to a broad set of structured and unstructured data sources through Spark APIs. With this capability, traditional z/OS data sources, such as IMS™, VSAM, IBM DB2®, z/OS, PDSE, or SMF data, can be accessed in a performance-optimized manner with Spark

This analytics example uses data stored in DB2 and VSAM tables, and a machine learning application written in [Scala](). The code also uses open-source [Jupyter Notebook](http://jupyter.org) to write and submit Scala code to your Spark instance, and view the output within a web GUI. The Jupyter Notebook is commonly used in data analytics space for data cleaning and transformation, numerical simulation, statistical modeling, machine learning and much more. 

<img src="images/spark_zOS.png" align="left"  width="100%" >
<br clear="all" />

## Included Components
The scenarios are accomplished by using:

- [IBM z/OS Platform for Apache Spark](http://www-03.ibm.com/systems/z/os/zos/apache-spark.html)  
- [Jupyter Notebook](http://jupyter-notebook.readthedocs.io/en/latest/)
- [Scala](https://www.scala-lang.org/documentation) 
- [IBM DB2 for z/OS](https://www.ibm.com/analytics/us/en/technology/db2/db2-for-zos.html) 
- [VSAM](https://www.ibm.com/support/knowledgecenter/zosbasics/com.ibm.zos.zconcepts/zconcepts_169.htm)   
   
## Prerequisites

Register at [z Systems Community Cloud](https://zcloud.marist.edu/#/register) for a trial account. You will receive an email containing credentials to access the self-service portal. This is where you can start exploring all the available services.   

## Steps

### Part A: Use Self-service Dashboard

1. [Start your Spark Cluster](#1-start-your-spark-cluster)
2. [Upload the DB2 and VSAM data](#2-upload-the-db2-and-vsam-data)
3. [Submit a Scala program to analyze the data](#3-submit-a-scala-program-to-analyze-the-data)
4. [Launch Spark GUI to view the submitted job](#4-launch-spark-gui-to-view-the-submitted-job)

### Part B: Work with Jupyter Notebook

5. [Launch Jupyter Notebook and connect to Spark](#5-launch-jupyter-notebook-and-connect-to-spark)
6. [Run Jupyter Notebook cells to load data and perform analysis](#6-run-jupyter-notebook-cells-to-load-data-and-perform-analysis)
      - 6.1 [Load VSAM and DB2 data into Spark and perform a data transformation](#6.1-load-vsam-and-db2-data-into-spark-and-perform-a-data-transformation)
      - 6.2 [Join the VSAM and DB2 data into dataframe in Spark](#6.2-join-the-vsam-and-db2-data-into-dataframe-in-spark)
      - 6.3 [Create a logistic regression dataframe and plot it](#6.3-create-a-logistic-regression-dataframe-and-plot-it)
      - 6.4 [Get statistical data](#6.4-get-statistical-data)

## Part A: Use Self-service Dashboard 

### 1. Start your Spark Cluster

1.Open a web browser and enter the URL to access the [z Systems Community Cloud](https://zcloud.marist.edu) self-service portal. 

<img src="images/Login.png" align="left" height="30%" width="30%" >
<br clear="all" />
<br/>

2.Enter your Portal User ID and Portal Password, and click ‘Sign In’.  

3.You will see the home page for the z Systems Community Cloud self-service portal.  
* **Click on ‘Try Analytics Service’**   

<img src="images/Trial.png" align="left" height="30%" width="30%" >
<br clear="all" />
<br/>

4.You will now see a dashboard, which shows the status of your Apache Spark on z/OS instance. 

At the top of the screen, notice the ‘z/OS Status’ indicator, which should show the status of your instance 
as ‘OK’. 

In the middle of the screen, the ‘Spark Instance’, ‘Status’, ‘Data management’, and ‘Operations’ sections 
will be displayed. The ‘Spark Instance’ section contains your individual Spark username and IP address. 

Below the field headings, you will see buttons for functions that can be applied to your instance.    
![GUI](images/Screen.png) 

The following table lists the operation for each function:   
<img src="images/Table.png" align="left" width="60%"  maxwidth="100%" >
<br clear="all" />
<br/>

5.If it is the first time for you to try the Analytics Service on zOS, you must set a new Spark password.
* **Click ‘Change Password’** 

<img src="images/Pwd.png" align="left" height="30%" width="30%" >
<br clear="all" />
<br/>

6.Confirm your instance is Active. If it is ‘Stopped’, click ‘Start’ to start it.   
<img src="images/Start.png" align="left" height="30%" width="30%" >
<br clear="all" />

### 2. Upload the DB2 and VSAM data

1.Go to https://github.com/cloud4z/spark and download all the sample files.   

2.The DB2 data for this exercise has already been loaded for you, no further action is required. However, you may upload the DDL and DB2 data file you downloaded as a prerequisite again, from your local system :   
* **Click ‘Upload Data’**   
* **Select and load the DB2 DDL file**   
* **Select and load the DB2 data file**   
* **Click ‘Upload’**   

<img src="images/Upload.png" align="left" height="30%" width="30%" >
<br clear="all" />

“Upload Success” will appear in the dashboard when the data load is complete. The VSAM data for this exercise has already been loaded for you. However, this step may be repeated by loading the VSAM copybook and VSAM data file you downloaded, from your local system.   

### 3. Submit a Scala program to analyze the data

Submit a prepared Scala program to analyze the data.    
* **Click ‘Spark Submit’**   
* **Select your Spark Demo JAR file**       
* **Specify Main class name ‘com.ibm.scalademo.ClientJoinVSAM’**     
* **Enter the arguments:  ‘Spark Instance Username’ ‘Spark Instance Password’**   
* **Click ‘Submit’**   
Note: The arguments suggest you need to login to the GUI to view the job results.  

<img src="images/Submit.png" align="left" height="40%" width="40%" >
<br clear="all" />

“JOB Submitted” will appear in the dashboard when the program is complete. This Scala program will access DB2 and VSAM data, perform transformations on the data, join these two tables in a Spark dataframe, and store the result back to DB2.

### 4. Launch Spark GUI to view the submitted job

Launch your individual Spark worker output GUI to view the job you just submitted.   
* **Click ‘Spark UI’**       
* **Click on the ‘Worker ID’ for your program in the ‘Completed Drivers’ section.**     
* **Log in with your Spark username and Spark password. The ones mentioned in step 6.**    
* **Click on ‘stdout’ for your program in the ‘Finished Drivers’ section to view your results.**     

!<img src="images/Auth.png" align="left" height="40%" width="40%" >
<br clear="all" />


## Part B: Work with Jupyter Notebook

### 5. Launch Jupyter Notebook and connect to Spark

Jupyter Notebook tool that is installed in the dashboard. This tool will allow you to write and submit Scala code to your Spark instance, and view the output within a web GUI.  

1.**Launch the Jupyter Notebook service in your browser from your dashboard.**
* **Click on ‘Jupyter’.**      
You will see the Jupyter home page.  

![Jupyter](images/Jupyter.png)

The prepared Scala program in this level will access DB2 and VSAM data, perform transformations on the data, join these two tables in a Spark dataframe, and store the result back to DB2. It will also perform a logistic regression analysis and plot the output.   

2. **Double click the Demo.jpynb file.**   

![Jupyter File Select](images/Select.png)

The Jupyter Notebook will connect to your Spark on z/OS instance automatically and will be in the ready state when the Apache Toree –Scala indicator in the top right hand corner of the screen is clear.     
<img src="images/clear.png" align="left" height="80%" width="80%" >
<br clear="all" />
### 6. Run Jupyter Notebook cells to load data and perform analysis
The Jupyter Notebook environment is divided into input cells labelled with ‘In [#]:’.      
#### 6.1 Load VSAM and DB2 data into Spark and perform a data transformation   <a name="6.1-load-vsam-and-db2-data-into-spark-and-perform-a-data-transformation"></a>
Run cell #1 - The Scala code in the first cell loads the VSAM data (customer information) into Spark and performs a data transformation.     
* **Click on the first ‘In [ ]:’**  
The left border will change to blue when a cell is in command mode, as shown below.    

<img src="images/highlight.png" align="left" height="80%" width="80%" >
<br clear="all" />

&nbsp;&nbsp;Before running the code, make the fllowing changes:
* **Change the value of zOS_IP to your Spark IP address.**      
* **Change the value of zOS_USERNAME to your Spark username and the value of zOS_PASSWORD to your Spark password.**     

![Change code](images/ChangeCode.png)

* **Click the run cell button indicated by the red box as shown below**

<img src="images/Run.png" align="left" height="80%" width="80%" >
<br clear="all" />

The Jupyter Notebook connection to your Spark instance is in the busy state when the Apache Toree –Scala indicator in the top right hand corner of the screen is grey. 

<img src="images/clear2.png" align="left" height="80%" width="80%" >
<br clear="all" />

When this indicator turns clear, the cell run has completed and returned to the ready state.  
The output should be similar to the following: 

<img src="images/out1.png" align="left" height="80%" width="80%" >
<br clear="all" />

Run cell #2 - The Scala code in the second cell loads the DB2 data (transaction data) into Spark and performs a data transformation.

    Note:  If you would like to use your own DDL and DB2 data, please first follow 
    the steps to upload DB2 data in Part A, and then edit the code in cell #2.

    Change

    option("dbtable", "sparkdb.sppaytb1").load()

    to
    
    option("dbtable", "[Your Table Name From Your DDL]").load()

* **Click on the next ‘In [ ]:’ to select the next cell**
* **Click the run cell button**
The output should be similar to the following:  

<img src="images/out2.png" align="left" height="80%" width="80%" >
<br clear="all" />

#### 6.2 Join the VSAM and DB2 data into dataframe in Spark   <a name="6.2-join-the-vsam-and-db2-data-into-dataframe-in-spark"></a>  
Run cell #3 - The Scala code in the third cell joins the VSAM and DB2 data into a new ‘client_join’ dataframe in Spark.
* **Click on the next ‘In [ ]:’ to select the next cell**
* **Click the run cell button**
The output should be similar to the following:      
<img src="images/out3.png" align="left" height="80%" width="80%" >
<br clear="all" />

#### 6.3 Create a logistic regression dataframe and plot it  <a name="6.3-create-a-logistic-regression-dataframe-and-plot-it"></a>
Run cell #4 - The Scala code in the fourth cell performs a logistic regression to evaluate the probability of customer churn as a function of customer activity level. The ‘result_df’ dataframe is also created, which is used to plot the results on a line graph.
* **Click on the next ‘In [ ]:’ to select the next cell**
* **Click the run cell button**
The output should be similar to the following:   
<img src="images/out4.png" align="left" height="40%" width="40%" >
<br clear="all" />
<br clear="all" />

Run cell #5 - The Scala code in the fifth cell plots the ‘plot_df’ dataframe.
* **Click on the next ‘In [ ]:’ to select the next cell**
* **Click the run cell button**   
The output should be similar to the following:
<img src="images/out5.png" align="left" height="60%" width="60%" >
<br clear="all" />

#### 6.4 Get statistical data <a name="6.4-get-statistical-data"></a>
a. The number of rows in the input VSAM dataset
* **println(clientInfo_df.count())**
Result should be 6001.
b. The number of rows in the input DB2 dataset
* **println(clientTrans_df.count())**
Result should be 20000.
c. The number of rows in the joined dataset
* **println(client_df.count())**
Result should be 112.


## Reference
IBM z/OS Platform for Apache Spark - http://www-03.ibm.com/systems/z/os/zos/apache-spark.html   
