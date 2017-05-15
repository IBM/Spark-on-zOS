# Spark-on-zOS
In this jurney we demonstrate running an analytics application using Spark on z/OS. This analytics example uses data stored in DB2 and VSAM tables, and a machine learning application written in Scala. 

z/OS is a 64-bit operating system for IBM mainframes, produced by IBM.
Apache Spark is an open-source cluster-computing framework.
Spark runs on Hadoop, Mesos, standalone, or in the cloud. It can access diverse data sources including HDFS, Cassandra, HBase, and S3. You can run Spark using its standalone cluster mode, on EC2, on Hadoop YARN, or on Apache Mesos.

Apache Spark on z/OS is in-place, optimized abstraction and real-time analysis of structured and unstructured enterprise data which is powered by z Systems Community Cloud.

## Part A: Self-service Dashboard
1.Register at http://www-03.ibm.com/systems/z/resources/trials.html for a trial account.   
Choose Apache Spark on z/OS trial   
2.Open a web browser and enter the URL to access the z Systems Community Cloud self-service portal.   
3.Enter your Portal User ID and Portal Password, and click ‘Sign In’.  
4.You will see the home page for the z Systems Community Cloud self-service portal.  
Click on ‘Try Analytics Service’   
5.You will now see a dashboard, which shows the status of your Apache Spark on z/OS instance. 
At the top of the screen, notice the ‘z/OS Status’ indicator, which should show the status of your instance as ‘OK’. In the middle of the screen, the ‘Spark Instance’, ‘Status’, ‘Data management’, and ‘Operations’ sections will be displayed. The ‘Spark Instance’ section contains your individual Spark username and IP address.   
Below the field headings, you will see buttons for functions that can be applied to your instance.   
6.If it is the first time for you to try the Analytics Service on zOS. Please reset the spark instance password (click the red "change password" button in the "Spark Instance" column).    
7.Confirm your instance is Active. If it is ‘Stopped’, click ‘Start’ to start it.   
8.Go to https://github.com/cloud4z/spark and download all the sample files.   
9.Load the DB2 data file :   
Click ‘Upload Data’    
Select and load the DB2 DDL file   
Select and load the DB2 data file   
Click ‘Upload’   
This will create the appropriate DB2 table for analysis.   
10.Submit a prepared Scala program to analyze the data.    
Click ‘Spark Submit’    
Select your Spark Demo JAR file   
Specify Main class name ‘com.ibm.scalademo.ClientJoinVSAM’   
Enter the arguments: Username Password   
Click ‘Submit’ 
Note: The arguments suggests you need to login to the GUI to view the job results. 
11.Launch your individual Spark worker output GUI to view the job you just submitted.   
Click ‘Spark UI’     
Click on the ‘Worker ID’ for your program in the ‘Completed Drivers’ section.   
Log in with your Spark username and Spark password. The ones mentioned in step 6.  
Click on ‘stdout’ for your program in the ‘Finished Drivers’ section to view your results.   
## Part B: Working with Jupyter Notebook
Jupyter Notebook tool that is installed in the dashboard. This tool will allow you to write and submit Scala code to your Spark instance, and view the output within a web GUI.   

