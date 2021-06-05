
## Machine Learning- Week2

### The Machine learning model based on the new dataset:
RandomForest Classifier from ML sklearn library

Based on the new dataset, our ML model predicts if a patient recovers or not from Covid based on the data we have.The dataset lacks continues features that could have a big  impact on our predications. 
These features could be different factors of existing health conditions such as preconditins( Diabetes, heart conditions, asthma,etc).Our data is limited to very few factores such as age, gender, location and date that have low corrolated to our outcome.

### Cleaning and Processing:
- Dropped unnecessary columns that had no impact on our predictation:
- Renamed the column names
- Converted Date to an ordinal Day by using toordinal function.
- Checked the categorial features and generated variable list
- Check the unique value counts for PHU_ID to see if binning is required
- Plot the density of value count of PHU_ID to determine what values to replace.

 ![PHU Density](Images/PHU_density.png)
 
 - Binned all PHU_IDs with less than 400 to keep the number of features at 10
- Converted the categorial features to continues by using OneHotEncoder from SKlearn library
- Merged the dataframes and dropped the categorial columns

### Set the Target and features
- Removed rows with 'Not resolved' in 'Outcome'  column to create two classes of 'Fatal' and 'Resolved'.The reason for remiving 'Not Resolved' was that this case could end up with either 'Resolved' or 'Fatal' later.
- Set 'Resolved' cases as our target(y)
- Removed the Outcome column from our dataframe to set up our features (X)

### Training and testing set:  
- Split our data into training and testing by train_test_split function from sklearn library
- Scaled the data by using StandardScaler

### RandomForest Classifier ML model:
- Accuracy score 0.908 - The high accuracy is due to high recovery rate of covid.

### Confusion Matrix
![confusion Matrix](Images/Confusion_matrix.png)

The recall and precison look low due to lack of contributing factors. According to the confusion matrix, model has predicted 209 to be Fatal out of 3152 cases.The actual fatal cases were 194 and 29% of the cases or 57 cases were correctly predicted. 


### Reasons for using RandomForest Classifier:

- It reduces overfitting in decision trees that improves high accuracy
- The model is robust to outliers.
- It works well with both categorial and continues values.  
- There are also low correlations in features that requires multiple learning algorithms.
- It automates missing values in the data.
 
### Limitations:

- Training large number of deep trees costs higher in terms of computing and memory usage
- More difficult to interpret comapares to individual decision trees 
- It has poorperformance on imbalanced data  

## Database

The general process that we will be following is as shown below:

![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/faridah/ETL%20Process.PNG)

### Extract

During the Extract process, we pull data from our two data sources i.e. Status of Cases per PHU (Public Health Unit) and Geographical Locations of PHUs using Python and Jupyter Notebooks.

![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/faridah/Extract.PNG)

### Transform

Once the data is extracted, we will be joining the data via the PHU_ID column and performing transformation using Python and Pandas. The primary aim of the transformation process is to transform the data into a consistent structure.

### Load

Finally, data will be loaded into a PostgreSQL database for easy distribution. SQL databases are often the targets of ETL processes, and because SQL is so ubiquitous, even databases that don't use SQL often have SQL-like interfaces.

![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/faridah/ETL_Whole.PNG)

## Database- ERD

Our dataset titled “Confirmed positive cases of COVID19 in Ontario” found here https://data.ontario.ca/dataset/confirmed-positive-cases-of-covid-19-in-ontario/resource/455fd63b-603d-4608-8216-7d8647f43350
contained 524,950 data points. Since the file was very large, we decided to do a random sample of the data and use this smaller dataset in our analysis. We then split the data into four different tables, cleaned and preprocessed the tables and created the following ERD to use as our blueprint for our database.

<img width="1338" alt="Covid19_PHU_ERD1" src="https://user-images.githubusercontent.com/75905911/119560169-95f8d980-bd71-11eb-9856-01d72383ade1.png">

<img width="1304" alt="Covid19_PHU_ERD2" src="https://user-images.githubusercontent.com/75905911/119560180-98f3ca00-bd71-11eb-9926-755b8e07d208.png">


The first table PHU_Locations contains the following columns: id, PHU_id (primary key), Reporting_PHU, Reporting_PHU_Address, Reporting_PHU_Latitude and PHU_Longitude. The second table PHU has the following columns: id (primary key), age_group, gender, outcome, outbreak, phu_id (foreign key), week, month, year. The columns for the third table, PHU_Gender_final are: index, phu_id (foreign key), gender, gender_count. Lastly, the fourth table called PHU_Age_Group_Final contains the following columns: index, phu_id (foreign key) and age_group_count.

## Database Storage
A database instance was created on AWS’ RDS and buckets were created on AWS’ S3 to hold all four tables.

<img width="1082" alt="AWS RDS" src="https://user-images.githubusercontent.com/75905911/119559642-f2a7c480-bd70-11eb-81bd-8575e47d3c99.png">

<img width="1110" alt="AWS S3" src="https://user-images.githubusercontent.com/75905911/119559660-f9ced280-bd70-11eb-9c77-85b4c9e519b5.png">

## Connection String
To connect our database, we used SQLAlchemy’s create engine

<img width="1381" alt="Connection String" src="https://user-images.githubusercontent.com/75905911/119559713-09e6b200-bd71-11eb-959b-462f747fbfcf.png">


## pgAdmin Database
Our four tables and their corresponding data were imported to pgAdmin.
The following is our sql for table creation:

<img width="585" alt="Screen Shot 2021-05-25 at 4 01 57 PM" src="https://user-images.githubusercontent.com/75905911/119560970-99409500-bd72-11eb-9b0d-9ea81cd44e75.png">

<img width="548" alt="Screen Shot 2021-05-25 at 4 02 50 PM" src="https://user-images.githubusercontent.com/75905911/119561049-b1181900-bd72-11eb-91f7-8c76d8b19a10.png">

<img width="570" alt="Screen Shot 2021-05-25 at 4 03 22 PM" src="https://user-images.githubusercontent.com/75905911/119561087-c12ff880-bd72-11eb-9904-cceaf3a8ff09.png">

<img width="584" alt="Screen Shot 2021-05-25 at 4 03 46 PM" src="https://user-images.githubusercontent.com/75905911/119561139-d0af4180-bd72-11eb-8077-6420c49713f2.png">


And images for our tables with data:
<img width="926" alt="PHU_locations" src="https://user-images.githubusercontent.com/75905911/119559854-33074280-bd71-11eb-9329-b5cf19da85fb.png">

<img width="1067" alt="phu" src="https://user-images.githubusercontent.com/75905911/119559821-2aaf0780-bd71-11eb-81a4-6d1cfcb17753.png">

<img width="474" alt="phu_gender_final" src="https://user-images.githubusercontent.com/75905911/119559849-30a4e880-bd71-11eb-8b03-d13f02aeb44c.png">

<img width="495" alt="phu_age_group_final" src="https://user-images.githubusercontent.com/75905911/119559835-2da9f800-bd71-11eb-96ea-424241034d8e.png">


## pgAdmin Table Join
We created 3 joined taables. All three tables were created with inner joins. The first, was a join of all four tables. The SQL code is here:
<img width="577" alt="Screen Shot 2021-05-25 at 4 07 08 PM" src="https://user-images.githubusercontent.com/75905911/119561524-49ae9900-bd73-11eb-8d8c-41523a9e20ce.png">


And an image of the table with the data can be seen here:
<img width="1141" alt="phu_joined1" src="https://user-images.githubusercontent.com/75905911/119559938-50d4a780-bd71-11eb-9279-8930bb3c4b1a.png">
<img width="1146" alt="phu_joined2" src="https://user-images.githubusercontent.com/75905911/119559952-53370180-bd71-11eb-93ee-719e319c66e4.png">


The second table called "phu_by_age_and_outcome" was created by joining the phu_locations, phu and phu_age_group_final tables. The sql can be seen here:

<img width="640" alt="phu_by_age_and_outcome" src="https://user-images.githubusercontent.com/75905911/119880776-9670ac00-befa-11eb-8920-9e36496aca8b.png">


And an image of the table:
<img width="1091" alt="phu_by_age_and_outcome" src="https://user-images.githubusercontent.com/75905911/119879902-b6ec3680-bef9-11eb-8f79-191951a1fe4e.png">


The third table we created is called "phu_by_gender_and_outcome" was created by joining phu_locations, phu and phu_gender_final tables. The SQL for the new table is:

<img width="577" alt="phu_by_gender_and_outcome" src="https://user-images.githubusercontent.com/75905911/119880078-e13df400-bef9-11eb-8de1-acae1db62c3e.png">


And an image of the table:
<img width="1073" alt="phu_by_gender_and_outcome" src="https://user-images.githubusercontent.com/75905911/119879939-c10e3500-bef9-11eb-8175-eafed7f30472.png">


=======
- Binned all PHU_IDs with less than 400 to keep the number of features at 10
- Converted the categorial features to continues by using OneHotEncoder from SKlearn library
- Merged the dataframes and dropped the categorial columns

### Set the Target and features
- Removed ' Not recivered' from outcome so we end up with two classes 'Fatal' and 'Recovered'
- Set Fatal cases as our target(y)
- Removed three columns ( fatal cases and resolved cases) from our dataframe to set up our features (X)

### Training and testing set:  
- Split our data into training and testing by train_test_split function from sklearn library
- Scaled the data
### RandomForest Classifier ML model:
- Accuracy score 0.915 - The high accuracy is due to high recovery rate of covid.

### Confusion Matrix
![confusion Matrix](Images/Confusion_matrix.png)

### Reasons for using RandomForest Classifier:

- It reduces overfitting in decision trees that improves high accuracy
- The model is robust to outliers.
- It works well with both categorial and continues values.  
- There are also low correlations in features that requires multiple learning algorithms.
- It automates missing values in the data.
 


### Limitations:

- Training large number of deep trees costs higher in terms of computing and memory usage
- More difficult to interpret comapares to individual decision trees 
- It has poorperformance on imbalanced data  


# Data Visualization using Tableau
### Overview of Covid Cases
The image below shows the total number of cases, number of cases based on age group, gender and status.
![Ontario Public Health Unit Covid Statistics (3)](https://user-images.githubusercontent.com/76136277/120877196-265dc800-c583-11eb-9925-1779e0df8bd2.png)

### Cases by Age Group and Public Health Unit 
This image shows the number of cases by Public Health Unit ID vs Age group. 
![Ontario Public Health Unit Covid Statistics (3)](https://user-images.githubusercontent.com/76136277/120877207-3c6b8880-c583-11eb-84f4-baf4a13dea91.png)

### Cases by Public Health Unit
The image was created using tableau map. It shows the number of cases by public health unit. The larger the size, the larger the number of cases. The second image also shows ![Ontario Public Health Unit Covid Statistics](https://user-images.githubusercontent.com/76136277/120877233-6a50cd00-c583-11eb-8d64-1f9dd6161459.png)

### Overview of Cases by Status
The image below represents covid status, that is, number of fatal, resolved and not resolved cases by age group, gender and PHU.
![Ontario Public Health Unit Covid Statistics (1)](https://user-images.githubusercontent.com/76136277/120877171-f8788380-c582-11eb-8183-29a493b04c37.png)
