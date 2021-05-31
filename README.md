<p align="center">
  <img width="650" height="163" src="https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/Logo.png?raw=true">
</p>

# Covid-19 and Public Health Units in Ontario

## Overview
This project is to showcase the strategical thinking and group efforts to predict and analyze the Covid-19 data. It is to recognize the trends of the highs and lows of Covid 19 cases at each of the 34 Public Health Unit in Ontario, Canada.<br>
<br>
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

# Research goal
***How do we determine the eligibility to excute a vaccination roll-out program?***

The goal of this analysis is to create a standard operating procedure (SOP) to determine a vaccine roll-out program.   The process stated here is to assist the Ministry of Health to identify, prioritize and execute vaccinations based on age group and or gender for future epidemics and pandemics.  <br>
Data of current confirmed Covid-19 cases have been collected and used to create a machine learning model that can provide predictions and help understand the probability of higher cases within a specific attribute of demographics.  <br>
The same data has been used for exploratory analysis to isolate results of each age group and gender for each Public Health Units.  <br>
Below are the steps taken to provide results for this analysis.

<br>
**Data source:**<br>
<br>

[Ontario Data Catalogue](https://data.ontario.ca/dataset/confirmed-positive-cases-of-covid-19-in-ontario/resource/455fd63b-603d-4608-8216-7d8647f43350)

## Extract, Transform & Load

The original data downloaded had 527,180 records which is a much larger file to work with and push in github.  Therefore the dataset has been scaled down using a random sample method and creating a [sample_covid_dataset.csv](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Datasource/sample_covid_dataset.csv), resulting in 13,524 records.<br>
This sampled dataset has been used for the database, machine learning model and the exploratory analysis.
<br>
Each team member has used the ETL process and saved work under their respective branches to show different perspectives if any.  

The general process that we will be following is as shown below:

![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/ETL%20Process.PNG?raw=true)

### Extract:

For the extract process, the sample dataset was pulled and read using Pandas in Python in a Jupyter notebook file.  Allowing the team to use multiple libraries to transform the  data for required purposes.

### Transform:

The transformation process was required to clean data.  The primary aim of the transformation process is to transform the data into a consistent structure.<br>
  - Drop any columns deemed unnecessary to the analysis <br>
  - Drop any null values<br>
  - Renaming column names for efficiency<br>
  - Separating the case date column into week, month and year <br>
  - Filter for specific requirements to be used for each part of project. <br>


### Load:

Finally, data will be loaded into a PostgreSQL database for easy distribution. SQL databases are often the targets of ETL processes, and because SQL is so ubiquitous, even databases that don't use SQL often have SQL-like interfaces.  The dataset will also be used for the project dashboard. <br>
<br>
![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/ETL_Whole.PNG?raw=true)
<br>


## Database 
After the cleaning and preprocessing of the dataset, the [cleaned_dataset](https://github.com/UofT-Government-Project/Covid19_PHU/blob/Week_2/Datasource/PHU_dataset_cleaned_michelle.csv) was split into four different tables.  Below is the ERD as a blueprint for the database, establishing the relationships created for each table.

### ERD:

[!ERD](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/ERD%20FINAL2/Covid19_PHU_ERD1.png?raw=true)<br>
[!ERD](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/ERD%20FINAL2/Covid19_PHU_ERD2.png?raw=true)<br>
<br>

### PostgreSQL Database:

The cleaned data was imported into a SQL database, Postgres using pgAdmin.  Using queries, a table named "phu" was created to host the entire dataset.  Further queries and fitering the main table, additional tables were created as well and then saved as csv files; [PHU_locations.csv](https://github.com/UofT-Government-Project/Covid19_PHU/blob/michelle/Covid19_Datasources/PHU_locations.csv), [phu_age_group_final.csv](https://github.com/UofT-Government-Project/Covid19_PHU/blob/michelle/Covid19_Datasources/phu_age_group_final.csv) and [phu_gender_final.csv](https://github.com/UofT-Government-Project/Covid19_PHU/blob/michelle/Covid19_Datasources/phu_gender_final.csv).<br>
*[schema1.sql](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/schema1.sql) file shows the queries.*

Using the newly saved csv files, four more tables were created and their corresponding data imported with queries.<br>
<br>
*[schema2.sql](https://github.com/UofT-Government-Project/Covid19_PHU/blob/Week_2/schema2.sql) file shows the additional queries.*
<br>

**Tables from schema2.sql:**
1.  PHU_locations - details containing the name and ID associated for a specific PHU (Public Health Unit) along with the coordinates and physical address for all of 34 units.<br>
<br>
![Location](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/PHU_locations.png?raw=true)<br>
2.  PHU - details include the age groups, gender, outcome for each case and the week, month and year for each case associated with each PHU.  An index ID was included to create a primary key to call on during queries. <br>
<br> 
![PHU](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/phu.png?raw=true)<br>
<br>
3.  PHU_Gender_final - includes the gender and the count associated with each PHU ID. <br>
![Gender](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/phu_gender_final.png?raw=true)<br>
4.  PHU_Age_Group_Final - contains the age group per case associated with each PHU ID. <br>
![Age_group](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/phu_age_group_final.png?raw=true)<br>
<br>
### Joins:

Two more tables were created by joining tables using the inner join method:
  1.  phu_by_age_and_outcome <br>
<img width="640" alt="phu_by_age_and_outcome" src="https://user-images.githubusercontent.com/75905911/119880776-9670ac00-befa-11eb-8920-9e36496aca8b.png">

<img width="1091" alt="phu_by_age_and_outcome" src="https://user-images.githubusercontent.com/75905911/119879902-b6ec3680-bef9-11eb-8f79-191951a1fe4e.png">

  2.  phu_by_gender_and_outcome <br>

<img width="577" alt="phu_by_gender_and_outcome" src="https://user-images.githubusercontent.com/75905911/119880078-e13df400-bef9-11eb-8de1-acae1db62c3e.png">

<img width="1073" alt="phu_by_gender_and_outcome" src="https://user-images.githubusercontent.com/75905911/119879939-c10e3500-bef9-11eb-8175-eafed7f30472.png">

### Connection String:

To create a connection from the database into PostgreSql, the SQLAlchemy's create engine library was used to load the refined csv file.

<img width="1381" alt="Connection String" src="https://user-images.githubusercontent.com/75905911/119559713-09e6b200-bd71-11eb-959b-462f747fbfcf.png">

### Database Storage:

A database instance was created on AWS' RDS (relational database) and four buckets, one for each table, were created using S3 - a public cloud storage on AWS.

<img width="1082" alt="AWS RDS" src="https://user-images.githubusercontent.com/75905911/119559642-f2a7c480-bd70-11eb-81bd-8575e47d3c99.png">

<img width="1110" alt="AWS S3" src="https://user-images.githubusercontent.com/75905911/119559660-f9ced280-bd70-11eb-9c77-85b4c9e519b5.png">

## Machine Learning

For a machine learning model, particular steps need to be followed to ensure a successful model. <br>
<br>
![ML Flowchart](https://github.com/UofT-Government-Project/Covid19_PHU/blob/Week_1/Images/ML_flowchart.png?raw=true)  

### The Machine learning model: 

With the sample dataset, the machine learning model created is to predict a patient's probability of recovery from the Covid-19 virus based on the age group and gender.  <br>
Ideally a dataset with patients' health history, ie; existing health conditions, would allow the model to predict to it's fullest extent.  After alot of research for the ideal dataset, it was difficult to find one that includes other factors of a patient's health, to provide continuous features which would provide a better prediction.  This information may not be available to the general public assuming it would be a privacy issue.<br>  However based on the current dataset being the most relatable to the analysis and model, the current data is limited to age group and gender.  Therefore the RandomForest classifier (RFC) from ML sklearn library has been selected for the machine learning model.  

### Cleaning and Preprocessing:

Similar to the ETL process, the dataset was required to be cleaned and preprocessed to avoid errors in the prediction.  The following steps were:
  - dropped unnecessary columns that have no impact on the predictation
  - renamed the column names
  - converted 'Case Date' column to ordinal Day by using toordinal function
  - checked the categorial features and generated variable list
  - checked the unique value counts for PHU_ID to see if binning is required
  - plotted the density of value count of PHU_ID to determine what values to replace.

 ![PHU Density](Images/PHU_density.png)
 
  - binned all PHU_IDs with less than 400 to keep the number of features at 10
  - converted the categorial features to continues by using OneHotEncoder from sklearn library
  - merged the dataframes and dropped the categorial column

### Set the Target and features:

In order to focus the model's prediction to an outcome of "Recovered" or "Fatal, any rows with patients categorized as "Not Recovered" were removed.  These records would mean the case is still active and therefore not valid for a prediction. <br>
For the model, "Resolved" cases in the outcome column has been set as the target variable *(y)* and the remainder features set as *(X)* minus the outcome columns cases.

### Training and testing set:  

Following the named target and features, the data was then split to training and testing sets by using the train_test_split function from the sklearn library.  <br>
Furthermore both training and testing data sets were then scaled to normalize the data.

### RandomForest Classifier ML model:

***The reasons why this model was selected***
  - because it reduces the chances of overfitting by using decision trees which improves high accuracy
  - the model is robust to outliers
  - it works well with both categorical and continous values
  - the correlation between features are minimal and therefore reduces the number of multiple learning algorithms
  - it automates missing values in the data

### Model Results:

After running the model, the accuracy score is 0.908.  The high accuracy score is due to the higher rate of recovered cases.  <br>
Based on the Confusion Matrix below there are 3,152 Covid-19 cases used in the model.  The results identified:
  - out of 194 total fatal cases - 29% of the cases were predicted true and 71% were predicted falsely
  - out of 2,958 total resolved cases - 51% of the cases were predicted false and 49% were predicted correct.

![confusion Matrix](Images/Confusion_matrix.png)


### Limitations:

Though the RFC model has many positive attributes, there are some limitations in the performance. <br>
Training large number of deep trees can be expensive in terms of computing and memory usage required.  If the data was much more diverse, the model may not be able to interpret any comparision between individual decision trees.  The RFC model also cannot perform extensively with imbalanced data.

## Exploratory Analysis

In exploring the data with further analysis on Python, the results can identify and isolate specific information.  Such as:
  - Identifying the number of cases per age group.  Based on the pie chart below, the highest number of cases are within the 20 years of age at 14.7% and the lowest at 5.9% within the age of 70.<br>
![Covid_cases_by age_group](https://github.com/UofT-Government-Project/Covid19_PHU/blob/michelle/Visualizations/Covid_19_cases_by_age_group.png?raw=true)
<br>
  - Number of cases per gender.  This chart reveals females have been more of the victim for contracting Covid-19, at 54.1% vs. males at 45.1%. <br>
![Covid_cases_by gender](https://github.com/UofT-Government-Project/Covid19_PHU/blob/michelle/Visualizations/Covid_19_cases_by_gender.png?raw=true)
<br>
  - Cases by age and gender.  Below chart segregates the cases by gender and age.  Highest cases are females within the age of 40 and lowest are male in the ages of 90 +. <br>
![Cases by age_gender](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/age_gender.png?raw=true)
<br>
  - Percentage of fatalities per gender reveals a higher rate for females at 6.41%, this would be obvious due to higher number of cases in females. <br>
![Fatal_rates](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/fatal_by_gender.png?raw=true)
<br>

## Dashboard

An interactive dashboard will be created in the following week.  The dashboard will provide option to select a specific Public Health Unit which will then provide details of location, number of cases for that specific unit and isolated case numbers based on gender and age.  This will be created using plotly on JavaScript and displayed via HTML. <br>
<br>
Tableau will be used as well to create a dashboard which will highlight further charts and or graphs similar to above exploratory analysis.  All dashboards will be compiled together to create a storyboard that can be shared with public and or used to present.  Below are some of the images of analysis using Tableau.
<br>
  1.  Overview of Covid Cases
The image below shows the total number of cases, number of cases based on age group, gender and status.
![Overview of Covid Cases](https://user-images.githubusercontent.com/76136277/120117474-5a885180-c15b-11eb-80c2-7ffe892f8e8f.png)

  2.  Cases by Age Group and Public Health Unit 
This image shows the number of cases by Public Health Unit ID vs Age group. 
![Cases by Age Group_PHU ID](https://user-images.githubusercontent.com/76136277/120117532-ab984580-c15b-11eb-9409-5041b2cd4c5a.png)

  3.  Cases by Public Health Unit
The image was created using tableau map. It shows the number of cases by public health unit. The larger the size, the larger the number of cases.
![MAP](https://user-images.githubusercontent.com/76136277/120117926-b81d9d80-c15d-11eb-9996-4469401d308f.PNG)

## Presentation

A final presentation will be created that includes snapshots of the entire project that will be used as introduction.  
*This [Google_presentation](https://docs.google.com/presentation/d/1R-9hwFz2FQSbQqZFsBUwxTXCbG8xHMHgzqgI43Wb4a4/edit?usp=sharing) is a work in progress.*
