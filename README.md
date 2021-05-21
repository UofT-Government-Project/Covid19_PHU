
## Machine Learning- Week2


### The Machine learning model based on the new dataset:
RandomForest Classifier from ML sklearn library

Based on the new dataset,our prediction is the fatal cases of covid cases.The dataset lacks continues features that have an impact on our predications. 
These features could be different factors of health conditions.Our data is limited to very few factores such as age, gender, location and date that are not corrolated to our outcome.

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

## Overview
This project is to showcase the strategical thinking and group efforts in creating a maching learning model. It is to recognize the trends of the high and lows of Covid 19 cases for each Public Health Unit in Ontario, Canada.<br>
<br>
## Research goal
Two sets of data have been used for the machine learning model; these datasets will be providing a prediction of which Public Health Unit(s) may have a potential risk of higher active cases.  Understanding the probability of higher cases in advance would assist the Ministry of Health/Government to be proactive; setting a plan in place for allocating extra resources, support, budgeting or even consider opening an additional temporary units to avoid overwhelming the existing units.<br>
<br>
**Data source:**<br>
[Ontario Data Catalogue](https://data.ontario.ca/en/) - has available the [Status_of_Covid19_Cases_in_Ontario_by Public_Health_Unit_(PHU)](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Datasource/cases_by_status_and_phu.csv)<br>
[Ontario Geohub](https://geohub.lio.gov.on.ca/) - has available the geographical locations of [Ministry_of_Health - Public_Health_Unit_Boundary](https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Datasource/Ministry_of_Health_Public_Health_Unit_Boundary.csv).<br>
<br>
## Communication protocol
A group chat has been set up in Slack.  This will be the primary platform for ongoing correspondence by each team member while working on our individual roles for each segment.  Every Monday and Wednesday evenings will be an opportunity to meet via zoom and discussing the current week's agenda.  Every Sunday the team will connect via Google Meet as well to finalize the submission of the current week.  Additional meetings will be set up throughout the week when needed.<br>
Phone numbers have been exchanged and a group chat set up on WhatsApp for ad hoc communications as well. <br>
*Collaborators:* [Lida](https://github.com/lidajav), [Tarana](https://github.com/taranahassan), [Michelle](https://github.com/MichelleGoldfinger), [Blessing](https://github.com/Physsyb), [Faridah](https://github.com/faridah-m).

### Team Member roles:
***Tarana:***  Setting up and managing repository, branches and updating README.md.<br>
***Faridah:***  ETL of data.<br>
***Michelle:***  Setting up Database.<br>
***Lida:*** Creating the machine learning model to be used. <br>
***Blessing:***  Explanation of which technologies group will be using and why and presentation.<br>
<br>
## Extract, Transform & Load


### Set the Target and features
- Removed ' Not recivered' from outcome so we end up with two classes 'Fatal' and 'Recovered'
- Set Fatal cases as our target(y)
- Removed three columns ( fatal cases and resolved cases) from our dataframe to set up our features (X)


### Training and testing set:  
- Split our data into training and testing by train_test_split function from sklearn library
- Scaled the data
### RandomForest Classifier ML model:
- Accuracy score 0.92 - The high accuracy is due to high recovery rate of covid.


The general process that we will be following is as shown below:

![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/faridah/ETL%20Process.PNG)

### Extract:

During the Extract process, we pull data from our two data sources i.e. Status of Cases per PHU (Public Health Unit) and Geographical Locations of PHUs using Python and Jupyter Notebooks.

![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/faridah/Extract.PNG)

### Transform:

Once the data is extracted, we will be joining the data via the PHU_ID column and performing transformation using Python and Pandas. The primary aim of the transformation process is to transform the data into a consistent structure.

### Load:

Finally, data will be loaded into a PostgreSQL database for easy distribution. SQL databases are often the targets of ETL processes, and because SQL is so ubiquitous, even databases that don't use SQL often have SQL-like interfaces.

![Image](https://github.com/UofT-Government-Project/Covid19_PHU/blob/faridah/ETL_Whole.PNG)<br>
<br>
## Database Mock-Up
Two data sources were used to create the ERD for our project. The first dataset is the "Status of COVID-19 cases in Ontario by Public Health Unit (PHU)". Columns' details are: _id, FILE_DATE, PHU_NAME, PHU_NUM, ACTIVE_CASES, RESOLVED_CASES and DEATHS. The second dataset titled "Ministry of Health Public Health Unit Boundary" has the following columns: FID, OGF_ID, PHU_ID, NAME_ENG, NAME_FR, GEO_UPD_DT, EFF_DATE, Shape__Area, and Shape__Length.

### ERD:
<img width="1377" alt="Screen Shot 2021-05-16 at 3 34 26 PM" src="https://user-images.githubusercontent.com/75905911/118410241-76b8c880-b65c-11eb-895b-6b70acd25844.png">

Primary Keys for both tables are: _id for "Status of COVID-19 cases in Ontario by Public Health Unit (PHU)" and PHU_ID for "Ministry of Health Public Health Unit Boundary". Although the names of the columns are different, both columns hold the same numeric unique identifier for each Ontario Public Health Unit. PHU_ID is also a foreign key for "Ministry of Health Public Health Unit Boundary". The tables will be joined using the PHU_NUM and PHU_IDs columns from both tables since they contain the same unique identifiers. Other foreign key assignments are: PHU_NAME in "Status of COVID-19 cases in Ontario by Public Health Unit (PHU)" and NAME_ENG in "Ministry of Health Public Health Unit Boundary".

Once data is merged, cleaned and preprocessed we hope use AWS and ProstreSQL to store and share data. <br>
<br>
## Machine Learning


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



  


