# Spark-on-zOS
In this jurney we demonstrate running an analytics application using Spark on z/OS. This analytics example uses data stored in DB2 and VSAM tables, and a machine learning application written in Scala. 

z/OS is a 64-bit operating system for IBM mainframes, produced by IBM.
Apache Spark is an open-source cluster-computing framework.
Spark runs on Hadoop, Mesos, standalone, or in the cloud. It can access diverse data sources including HDFS, Cassandra, HBase, and S3. You can run Spark using its standalone cluster mode, on EC2, on Hadoop YARN, or on Apache Mesos.

Apache Spark on z/OS is in-place, optimized abstraction and real-time analysis of structured and unstructured enterprise data which is powered by z Systems Community Cloud.

## Part A: Self-service Dashboard 

1.Register at http://www-03.ibm.com/systems/z/resources/trials.html for a trial account.   
* **Choose Apache Spark on z/OS trial**      
You will receive an email containing credentials to access the self-service portal.  This is where you can start exploring all the available services.   

2.Open a web browser and enter the URL to access the z Systems Community Cloud self-service portal.   
![Login](img/Login.png)

3.Enter your Portal User ID and Portal Password, and click ‘Sign In’.  

4.You will see the home page for the z Systems Community Cloud self-service portal.  
* **Click on ‘Try Analytics Service’**      
![Trial](img/Trial.png)

5.You will now see a dashboard, which shows the status of your Apache Spark on z/OS instance. 

At the top of the screen, notice the ‘z/OS Status’ indicator, which should show the status of your instance 
as ‘OK’. 

In the middle of the screen, the ‘Spark Instance’, ‘Status’, ‘Data management’, and ‘Operations’ sections 
will be displayed. The ‘Spark Instance’ section contains your individual Spark username and IP address. 

Below the field headings, you will see buttons for functions that can be applied to your instance.    
![GUI](img/Screen.png) 
The following table lists the operation for each function:   
![Table](img/Table.png)

6.If it is the first time for you to try the Analytics Service on zOS, you must set a new Spark password.
* **Click ‘Change Password’**   
![Change Password](img/Pwd.png)

7.Confirm your instance is Active. If it is ‘Stopped’, click ‘Start’ to start it.   
![Start](img/Start.png)

8.Go to https://github.com/cloud4z/spark and download all the sample files.   

9.Load the DB2 data file :   
* **Click ‘Upload Data’**   
* **Select and load the DB2 DDL file**   
* **Select and load the DB2 data file**   
* **Click ‘Upload’**   
![Upload](img/Upload.png)

“Upload Success” will appear in the dashboard when the data load is complete. The VSAM data for this exercise has already been loaded for you. However, this step may be repeated by loading the VSAM copybook and VSAM data file you downloaded, from your local system.   

10.Submit a prepared Scala program to analyze the data.    
* **Click ‘Spark Submit’**   
* **Select your Spark Demo JAR file**       
* **Specify Main class name ‘com.ibm.scalademo.ClientJoinVSAM’**     
* **Enter the arguments: Username Password**   
* **Click ‘Submit’**   
Note: The arguments suggest you need to login to the GUI to view the job results.  
![Submit](img/Submit.png)
“JOB Submitted” will appear in the dashboard when the program is complete. This Scala program will access DB2 and VSAM data, perform transformations on the data, join these two tables in a Spark dataframe, and store the result back to DB2.

11.Launch your individual Spark worker output GUI to view the job you just submitted.   
* **Click ‘Spark UI’**       
* **Click on the ‘Worker ID’ for your program in the ‘Completed Drivers’ section.**     
* **Log in with your Spark username and Spark password. The ones mentioned in step 6.**    
* **Click on ‘stdout’ for your program in the ‘Finished Drivers’ section to view your results.**     
![Authentication](img/Auth.png) 


## Part B: Working with Jupyter Notebook
Jupyter Notebook tool that is installed in the dashboard. This tool will allow you to write and submit Scala code to your Spark instance, and view the output within a web GUI.  
1.Launch the Jupyter Notebook service in your browser from your dashboard.   
* **Click on ‘Jupyter’.**      
You will see the Jupyter home page.          

2.The prepared Scala program in this level will access DB2 and VSAM data, perform transformations on the data, join these two tables in a Spark dataframe, and store the result back to DB2. It will also perform a logistic regression analysis and plot the output.   
* **Select the Demo.jpynb file.**          
The Jupyter Notebook will connect to your Spark on z/OS instance automatically and will be in the ready state when the Apache Toree –Scala indicator in the top right hand corner of the screen is clear.     

3.The Jupyter Notebook environment is divided into input cells labelled with ‘In [#]:’.  
&nbsp;&nbsp;Before running the code, make the fllowing changes:
* **Change the value of zOS_IP to your Spark IP address.**      
* **Change the value of zOS_USERNAME to your Spark username and the value of zOS_PASSWORD to your Spark password.**      

4.Click each ‘In [#]:’ section, then click the run button in the GUI. Check out the results.

## Reference
IBM DB2 for z/OS - https://www.ibm.com/analytics/us/en/technology/db2/db2-for-zos.html   
VSAM - https://www.ibm.com/support/knowledgecenter/zosbasics/com.ibm.zos.zconcepts/zconcepts_169.htm   
IBM z/OS Platform for Apache Spark - http://www-03.ibm.com/systems/z/os/zos/apache-spark.html   
Jupyter Notebook - http://jupyter-notebook.readthedocs.io/en/latest/   
Scala - https://www.scala-lang.org/documentation   

