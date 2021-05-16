<p align="center">
  <img width="650" height="163" src="https://github.com/UofT-Government-Project/Covid19_PHU/blob/main/Images/Logo.png?raw=true">
</p>

# Covid-19 and Public Health Units in Ontario

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

Two sets of data have been used for the machine learning model; these datasets will be providing a prediction of which Public Health Unit(s) may have a potential risk of higher active cases. We have been tasked with combining these two datasets, cleaning the data so that all participants can use the final combined dataset and finally saving the data into a PostgreSQL database.

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
