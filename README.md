<p align="center">
  <img width="650" height="163" src="https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/Logo.png?raw=true">
</p>

# Covid-19 and Public Health Units in Ontario

## Overview
This project is to showcase the strategical thinking and group efforts to predict and analyze the Covid-19 data. It is to recognize the trends of the highs and lows of Covid 19 cases at each of the 34 Public Health Unit in Ontario, Canada.<br>
<br>
## Research goal
***How do we determine the eligibility to excute a vaccine roll-out program?***

The goal of this analysis is to create a standard operating procedure (SOP) to determine a vaccine roll-out program.   The process stated here is to assist the Ministry of Health to identify and prioritize executing vaccinations based on age group and or gender for future epidemics and pandemics.  <br>
Data of current confirmed Covid-19 cases have been collected and used to create a machine learning model that can provide predictions and help understand the probability of higher cases within a specific attribute of demographics.  <br>
The same data has been used for exploratory analysis to isolate results of each age group and gender for each Public Health Units.  <br>
Below are the steps taken to provide results for this analysis.

<br>
**Data source:**<br>

[Ontario Data Catalogue](https://data.ontario.ca/dataset/confirmed-positive-cases-of-covid-19-in-ontario/resource/455fd63b-603d-4608-8216-7d8647f43350)

## Communication protocol
A group chat has been set up in Slack.  This will be the primary platform for ongoing correspondence by each team member while working on our individual roles for each segment.  Every Monday and Wednesday evenings will be an opportunity to meet via zoom and discussing the current week's agenda.  Every Sunday the team will connect via Google Meet as well to finalize the submission of the current week.  Additional meetings will be set up throughout the week when needed.<br>
Phone numbers have been exchanged and a group chat set up on WhatsApp for ad hoc communications as well. <br>
*Collaborators:* [Lida](https://github.com/lidajav), [Tarana](https://github.com/taranahassan), [Michelle](https://github.com/MichelleGoldfinger), [Blessing](https://github.com/Physsyb), [Faridah](https://github.com/faridah-m).

### Team Member roles:
***Tarana:***  Managining github and creating interactive dashboard.<br>
***Faridah:***  Creating presentation on google slides<br>
***Michelle:***  Creating an ERD and database.<br>
***Lida:*** Creating the machine learning model. <br>
***Blessing:***  Creating dashboard using a BI tool.

## Extract, Transform & Load

The original data downloaded had 527,180 records which is a much larger file to work with and push in github.  Therefore the dataset has been scaled down using a random sample method and creating a [sample_covid_dataset.csv](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Datasource/sample_covid_dataset.csv), resulting in 13,524 records.<br>
This sampled dataset has been used for the database, machine learning model and the exploratory analysis.
<br>
Each team member has used the ETL process and saved work under their respective branches to show different perspectives if any.  

The general process that we will be following is as shown below:

![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/faridah/ETL%20Process.PNG)

### Extract:

For the extract process, the sample dataset was pulled and read using Pandas in Python in a Jupyter notebook file.  Allowing the team to use multiple libraries to transform the  data for required purposes.

### Transform:

The transformation process was required to clean data:<br>
  - drop any columns deemed unnecessary to the analysis <br>
  - drop any null values<br>
  - separating the case date column into week, month and year <br>
  - filter for specific requirements to be used for each part of project. <br>
The primary aim of the transformation process is to transform the data into a consistent structure.

### Load:

Finally, data will be loaded into a PostgreSQL database for easy distribution. SQL databases are often the targets of ETL processes, and because SQL is so ubiquitous, even databases that don't use SQL often have SQL-like interfaces.  The dataset will also be used for the project dashboard.
<br>
![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/faridah/ETL_Whole.PNG)


## Database 
After the cleaning and preprocessing of the dataset, the [cleaned_dataset](https://github.com/UofT-Government-Project/Covid19_PHU/blob/Week_2/Datasource/PHU_dataset_cleaned_michelle.csv) was split into four different tables.  Below is the ERD as a blueprint for the database, establishing the relationships created for each table.

### ERD:

<img width="1338" alt="Covid19_PHU_ERD1" src="https://user-images.githubusercontent.com/75905911/119560169-95f8d980-bd71-11eb-9856-01d72383ade1.png">

<img width="1304" alt="Covid19_PHU_ERD2" src="https://user-images.githubusercontent.com/75905911/119560180-98f3ca00-bd71-11eb-9926-755b8e07d208.png">

##### Tables:
1.  PHU_locations - details containing the name and ID associated for a specific PHU (Public Health Unit) along with the coordinates and physical address for all of 34 units.
2.  PHU - details include the age groups, gender, outcome for each case and the week, month and year for each case associated with each PHU ID.  An index ID was included to create a primary key to call on during queries.
3.  PHU_Gender_final - includes the gender and the count associated with each PHU ID.
4.  PHU_Age_Group_Final - contains the age group per case associated with each PHU ID.

### PostgreSQL Database

The above four tables and their corresponding data were imported into a SQL database, Postgres using pgAdmin.  Below are the sql schema images.
<img width="584" alt="Screen Shot 2021-05-25 at 4 01 57 PM" src="https://user-images.githubusercontent.com/75905911/119560970-99409500-bd72-11eb-9b0d-9ea81cd44e75.png"><img width="584" alt="Screen Shot 2021-05-25 at 4 02 50 PM" src="https://user-images.githubusercontent.com/75905911/119561049-b1181900-bd72-11eb-91f7-8c76d8b19a10.png"><img width="584" alt="Screen Shot 2021-05-25 at 4 03 22 PM" src="https://user-images.githubusercontent.com/75905911/119561087-c12ff880-bd72-11eb-9904-cceaf3a8ff09.png"><img width="584" alt="Screen Shot 2021-05-25 at 4 03 46 PM" src="https://user-images.githubusercontent.com/75905911/119561139-d0af4180-bd72-11eb-8077-6420c49713f2.png">
<br>

Below are the views of how each table is visualized.

<img width="926" alt="PHU_locations" src="https://user-images.githubusercontent.com/75905911/119559854-33074280-bd71-11eb-9329-b5cf19da85fb.png">

<img width="1067" alt="phu" src="https://user-images.githubusercontent.com/75905911/119559821-2aaf0780-bd71-11eb-81a4-6d1cfcb17753.png">

<img width="474" alt="phu_gender_final" src="https://user-images.githubusercontent.com/75905911/119559849-30a4e880-bd71-11eb-8b03-d13f02aeb44c.png">

<img width="495" alt="phu_age_group_final" src="https://user-images.githubusercontent.com/75905911/119559835-2da9f800-bd71-11eb-96ea-424241034d8e.png">

### Joins


### Connection String

To create a connection from the database into PostgreSql, the SQLAlchemy's create engine library was used to load the refined csv file.

<img width="1381" alt="Connection String" src="https://user-images.githubusercontent.com/75905911/119559713-09e6b200-bd71-11eb-959b-462f747fbfcf.png">

### Database Storage

A database instance was created on AWS' RDS (relational database) and four buckets, one for each table, were created using S3 - a public cloud storage on AWS.

<img width="1082" alt="AWS RDS" src="https://user-images.githubusercontent.com/75905911/119559642-f2a7c480-bd70-11eb-81bd-8575e47d3c99.png">

<img width="1110" alt="AWS S3" src="https://user-images.githubusercontent.com/75905911/119559660-f9ced280-bd70-11eb-9c77-85b4c9e519b5.png">

## Machine Learning

### The Machine learning model: 
RandomForest classifier (RFC) from ML sklearn library

### Training and testing set:  
Dates (broken into month and year), PHU (public health unit), location, number of Covid cases resolved and death cases per PHU.

### Target: 
Active cases.
The model is going to predict PHUs with high active cases to help the government for allocating budgets. 

### The reasons for choosing the ML model: 
The model has high accuracy and is robust to outliers. There are also low correlations in features that requires multiple learning algorithms. 

![ML Flowchart](https://github.com/UofT-Government-Project/Covid19_PHU/blob/Week_1/Images/ML_flowchart.png?raw=true)

## Machine Learning- Week2

### The Machine learning model based on the new dataset:
RandomForest Classifier from ML sklearn library

### Based on the new dataset, our ML model predicts if a patient recovers or not from Covid based on the data we have.The dataset lacks continues features that could have a big  impact on our predications. 
These features could be different factors of existing health conditions such as preconditins( Diabetes, heart conditions, asthma,etc).Our data is limited to very few factores such as age, gender, location and date that have low corrolated to our outcome.

### Cleaning and Processing:
- Dropped unnecessary columns that have no impact on our predictation:
 -Renamed the column names
 -Broke Date to week, month and year
 -Checked the categorial features
- Check the unique value counts for PHU_ID to see if binning is required
- Plot the density of value count of PHU_ID to determine what values to replace.
 ![PHU Density](Images/PHU_density.png)

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




  


