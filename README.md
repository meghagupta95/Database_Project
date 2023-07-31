# Database Project
## Introduction:

Project has the vision to add / compare performance on similar queries which are run on MongoDb and MySQL. For simplicity we have identified to leverage cloud infrastructure for this purpose. Initially in the document we are going over how to setup cluster in Atlas (Used for Mongo DB) and AWS RDS.

For apple to apple comparison in performance, both of the databases are deployed in AWS free tier version. The dataset chosen for the comparison is of Bank Loan defaulters. Since the same dataset is chosen for the comparison, metrics captured during the performance analysis adds more value.

In the document added below, you will find comparison in performance over several type of CRUD operations, and how to setup the cluster on AWS and Atlas.

## Gathering Data from Kaggle

Link to download source data: https://www.kaggle.com/datasets/gauravduttakiit/loan-defaulter?select=previous_application.csv


  *	It is the 3rd file, named - previous_applications.csv which we used.

The Source code files and the scripts which generates the data is in Google Drive . Please click on this link to get the files: 

https://drive.google.com/drive/folders/1FRgG9TJzm2nk_Ypwg5CkNPUEOiNftxOv?usp=sharing

## Data Wrangling

Data cleaning is done on Jupyter Notebook using python. We had more than a million records in the initial datasets but this much data is not supported in free tier of either of the databases that’s why we trimmed our data to 4 lakhs records.

We included Jupyter notebook containing the steps to clean the data (to remove the null values, renaming of columns) and to trim the data as much we required.

After running Jupyter file, we are extracting 4 lakh records from the entire data to perform operations.

Cluster Setup on Atlas and AWS

## Cluster setup for MongoDb on Atlas

* Register on Atlas and Create Cluster
    
    * Register on Atlas
        * Go to Mongo DB and register
            * URL: https://www.mongodb.com/
            * Register
               * Add details after clicking on Try Free

* Creation of Cluster
 
* Creation of Database and Collection in MongoDB Atlas

  ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/e31851ad-d9fe-4572-971e-18a7fdb31615)

* To connect to cluster, we can perform either of 3 options as given in below options:

* We downloaded, Mongodb shell to run the commands on terminal.

![image](https://github.com/meghagupta95/Database_Project/assets/99114628/6b5bb329-6624-4b28-815c-dfc748988306)

**Below image is showing created cluster containing BankLoan as a collection**
 
 For Mac:
 
   ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/249bd98f-15b3-4a43-b380-b252910bd28d)


For Windows:

  ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/13ba3b0e-bc7f-4479-931d-bab1a58d9b07)

  ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/79188da8-17b8-4aa6-bef1-417930bcfc2b)


**Command to upload dataset in Mongodb from terminal:**

    Command to upload:
          mongoimport —uri 
          mongodb+srv://megha:meghaabc@cluster0.gbgnc.mongodb.net/DatabaseProject — 
          collection BankLoan —type CSV —file ~/Downloads/project_dataset_4l.csv — 
          headerline
        
where DatabaseProject is database name, BankLoan is Collection name and -/Downloads/project_dataset_4l.csv. is file name

  
**Instance setup for AMAZON RDS on AWS**
 * Go to https://aws.amazon.com/rds/ > click on sign in to the new console.
 
 * Create a new AWS account

 * We used Free Tier to create a Instance on RDS

 * We can create instances in databases tab from left hand side as shown in below screenshot and we will be using below end point & port information from Connectivity and Security.

![image](https://github.com/meghagupta95/Database_Project/assets/99114628/390fb0bb-36a6-4be1-a9c6-f5d1747f8f87)


**Connection of Amazon RDS and MY SQL Workbench**
 * Put Connection Name
 * To upload the data from My sql workbench, we have to set up the connection.
 * Mysql Workbench > database > Manage connections > Advanced> In others > OPT_Local_INFILE=1 lastConnected=1652566905 serverVersion = 8.0.28
 
 ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/8db9c97c-c239-442c-9d23-ee29ed1b7d9a)

 * In Connection >

  ![Screen Shot 2023-07-31 at 12 09 58 PM](https://github.com/meghagupta95/Database_Project/assets/99114628/b0a8e0f0-793e-4ab4-9127-0aba8193ce21)


* Queries on My SQL Workbench to perform operations on RDS

  * Identify the list of databases and Use the Database
    
    

  * Command to upload the data from My SQL Workbench to Amazon RDS:

    **Insert Table query for MYSQL**

    ![Screen Shot 2023-07-31 at 12 15 40 PM](https://github.com/meghagupta95/Database_Project/assets/99114628/f6348d10-e60e-4ed4-a7bf-7ad671b7a9f5)


      * MySQL

        ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/2d9fee36-feff-4e45-b4f3-99adf7b9037c)

        ![Screen Shot 2023-07-31 at 12 17 17 PM](https://github.com/meghagupta95/Database_Project/assets/99114628/ac4c44ac-8df5-4908-bdb9-a216ae67000a)

       * Code to upload dataset in MySQL:**

        ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/bdacf5bd-629c-49ae-b577-99e9d9738525)

        ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/296a2002-abaa-4c76-b97d-378245c52cdf)


    * Code to run in MySQL:

       Select query: The LIMIT value can be changed for every test

       select * from BankLoan LIMIT 500;


    **MySQL insert many: for 500 records**

      ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/d4b997fa-42a0-480d-836e-7492fcdb5ef2)

      ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/1e14e589-81b8-44f2-8970-7de469bf1efb)

  **MySQL Insert query for 1 lakh record: The value of i (in WHILE i<500000)can be changed to test for different number of records**

  ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/714f395c-50d4-40d3-99d9-2aedfce6a599)

  **MySQL Update query:**

  ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/6ac49459-c480-4982-bcf3-c949875dfa85)

  ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/02fcc1a4-55a1-415f-aff9-ee6fa458308a)


  **MYSQL Delete query:**

  ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/cf765bb0-971e-4722-835d-9ac31578c590)

  ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/68202a55-1a3b-4d37-b89b-33619a87232b) 


  **MYSQL Index Query:**
   
    We have used NEW INDEX column as Index.

    ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/7c3fd3a3-8c34-4833-ac22-d0921277a29d)


  **Aggregate Query to run on MySQL:**

    SELECT WEEKDAY_APPR_PROCESS_START, COUNT(*) FROM BankLoan
    GROUP BY WEEKDAY_APPR_PROCESS_START;

    ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/f53192c9-1a61-4ef0-bbe0-5022fc0c638d)


## Queries on Mongoshell to perform operations on Atlas

**Identify the list of collections. (Tables in SQL)**
  
  * Command show collections

**Select / Find Query:**

* MongoDB

  * Simple Query to find all Data

  * (Just FYI) Query to perform:

    * Query to collection results: db.BankLoan.find()
    * Collection find with default set to 20 rows
    * Query to Set Default size to 20: DBQuery.shellBatchSize = 10;
    * Query to collection results: db.BankLoan.find()

  * Collection size set to 100, 000
 
    * Approach 1:
        * Query to Set Default size to 100, 000: DBQuery.shellBatchSize = 100000;

         ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/772be0ae-3047-4b34-9912-0264e86747bc)

        * Query to collection results: db.BankLoan.find()

    * Approach 2:
        * db.BankLoan.find().limit(100000);
       
        ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/e9530a7e-1d0a-4cfc-834d-89c64925d852)

    * Collection Size set to 400, 000

      * Query to Set Default size to 100, 000: DBQuery.shellBatchSize = 100000;
        
      * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/494080d5-a978-49ec-a8aa-934b6da16e17)

      * Query to collection results: db.BankLoan.find()

**Find / Select with Where Clause**

* MongoDB

 * Where With Single Clause
   
   * Query: db.BankLoan.find({WEEKDAY_APPR_PROCESS_START: 'THURSDAY'})

   * Count of rows returned: 59, 584
   
   * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/ae8c8ea5-048d-49d9-b5ed-e3e8ac53101d)

 
 * Where with And / Or Clause
   
   * OR Clause
     
    * Weekday set to Thursday or Monday

    * ![Screen Shot 2023-07-31 at 12 56 18 PM](https://github.com/meghagupta95/Database_Project/assets/99114628/d00f34bb-2f91-4b9b-8341-cab4e143072a)

    * Results shows the collections of result which has days set to either Monday or Thursday

    * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/73637cd6-2734-4285-89a0-986460099065)

    * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/6ac5cd29-9853-4c99-aed5-7158958dc8e4)

      * Query resulted number of rows:120,121

      * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/aa04b508-c183-47df-a6bc-c3a0ab4dfb3e)

    * Query to identify all the loan application which were applied on Thursday and had any flags raised with any prior application

    * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/cb2a3f5c-49c3-40f5-900d-82aeaf69181c)

    * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/3659014e-7252-4450-9f9c-b0ad7ac6edf0)

 **Insert Query**
 
Mongo DB: The value of i can be changed for test to change number of records of insert

* Mongodb insert:10000

  * for (let i = 1; i <= 10000; ++i) {

    db.BankLoan.insertOne({
  
    "NEWINDEX" : 399999 + i,
  
    "SK_ID_PREV" : 30000 +i,
  
    "SK_ID_CURR": 30000 + i ,
  
    "NAME_CONTRACT_TYPE" : "customer_loan" ,
  
    "AMT_APPLICATION": 10000 ,
  
    "WEEKDAY_APPR_PROCESS_START ": "Monday" ,
  
    " HOUR_APPR_PROCESS_START ": 20 +i ,
  
    " FLAG_LAST_APPL_PER_CONTRACT " : "y" ,
  
    " NFLAG_LAST_APPL_IN_DAY " : 100 ,
  
    " NAME_CASH_LOAN_PURPOSE " : "personal",
  
    " NAME_CONTRACT_STATUS " : "approved" ,
  
    "DAYS_DECISION " : 30 ,
  
    " NAME_PAYMENT_TYPE ": "cash" ,
  
    " CODE_REJECT_REASON " : "unknown",
  
    " NAME_CLIENT_TYPE " :"individual" ,
    
    "NAME_GOODS_CATEGORY " : "unknown",
    
    " NAME_PORTFOLIO ": "known" ,
    
    " NAME_PRODUCT_TYPE " : "LAL" ,
    
    " CHANNEL_TYPE ": "online" ,
    
    "SELLERPLACE_AREA ": 95110 +i ,
    
    " NAME_SELLER_INDUSTRY " : "investment" ,
    
    " NAME_YIELD_GROUP " : "group"
    
    })
    
    }

* Run this file myscript.js.txt from source code file in google doc.

 * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/27c82c51-1e0c-4f68-b4a3-1d25c42c5f0e)

**Delete Query**

* Mongo DB

  * Run this file deletescript.js from source code file in google doc.

   * Delete 100, 000

   * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/0ef72af9-300e-4dbb-aa83-b41bc4063a80)

   * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/84f373bc-b58b-45f0-901f-127ca6f63b54)


**Mongo DB Delete query to delete many records:**

  * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/35337e7f-907f-49c5-9381-54da8df31b8f)

  * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/db2f824d-228b-4bfc-9f71-c25523898e10)


**Update Query:**

  * Run this file update.js from source code file in google doc.

  * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/d12769f0-0814-463e-8309-74f5aa3401c4)


Queries to update various number of records : Please change the queries in update.js file to check for different number of records

![image](https://github.com/meghagupta95/Database_Project/assets/99114628/762d87e7-68d4-4d4d-abc3-81931daf4936)

  * Mongo DB:

    * Updated Collections: 39, 830

      * Query:

        ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/1c436b1e-e072-42be-a26f-2fc874eaf113)

    * Updated Collections: 74, 212

      * Query:

        ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/15ba858a-5917-4a6b-b113-dda82f88bc3c)

    * Updated Collections: 175, 572

      * Query: 

        ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/1d037980-a8d6-4998-b4dc-b73ca3027b3a)


**Group By Query:**

* Mongo DB

  * Group By Weekday

    * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/b9dc87f8-fead-424c-a10c-1436f2404581)

    * ![image](https://github.com/meghagupta95/Database_Project/assets/99114628/d1403ab8-0808-49a4-97cc-8d000af20e23)


**Creating Index in Mongodb using MOngoDBcompass**

Click on create index button to create new index. We have used NEWINDEX column as index

![image](https://github.com/meghagupta95/Database_Project/assets/99114628/9e3d7b15-198c-4c91-83b2-9989c4b32ac8)


**COMMAND TO RUN TO CONNECT TO MONGODB LOCAL INSTANCE :**

mongosh "mongodb://localhost:27017/database2" —file find.<filename>
 
The queries to run will remain the same for both databases.
