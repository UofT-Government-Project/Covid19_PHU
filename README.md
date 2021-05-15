# Covid-19 and Public Health Units in Ontario

## Communication protocol:
A group chat has been set up in Slack.  This will be the primary platform for ongoing correspondence by each team member while working on our individual roles for each segment.  Every Monday and Wednesday evenings will be an opportunity to meet via zoom and discussing the current week's agenda.  Every Sunday the team will connect via Google Meet as well to finalize the submission of the current week.  Additional meetings will be set up throughout the week when needed.<br>
Phone numbers have been exchanged and a group chat set up on WhatsApp for ad hoc communications as well. <br>
*Collaborators:* [Lida](https://github.com/lidajav), [Tarana](https://github.com/taranahassan), [Michelle](https://github.com/MichelleGoldfinger), [Blessing](https://github.com/Physsyb), [Faridah](https://github.com/faridah-m).


### Team Member roles:
***Tarana:***  Setting up repository, branches and updating README.md.<br>
***Faridah:***  Explanation of the ETL process on data.<br>
***Michelle:***  Creating an ERD for the mockup database to be used.<br>
***Lida:*** Creating the mockup machine learning model to be used. <br>
***Blessing:***  Explanation of which technologies group will be using and why.

## Database Mock-Up
Two data sources were used to create the ERD for our project. The first dataset is the "Status of COVID-19 cases in Ontario by Public Health Unit (PHU)". Columns' details are: _id, FILE_DATE, PHU_NAME, PHU_NUM, ACTIVE_CASES, RESOLVED_CASES and DEATHS. The second dataset titled "Ministry of Health Public Health Unit Boundary" has the following columns: FID, OGF_ID, PHU_ID, NAME_ENG, NAME_FR, GEO_UPD_DT, EFF_DATE, Shape__Area, and Shape__Length.


### ERD
<img width="1431" alt="ERD_Covid19_PHU" src="https://user-images.githubusercontent.com/75905911/118367051-d20c8d00-b56e-11eb-873a-722179cd5bea.png">


Primary Keys for both tables are: PHU_NUM for "Status of COVID-19 cases in Ontario by Public Health Unit (PHU)" and PHU_ID for "Ministry of Health Public Health Unit Boundary". Although the names of the columns are different, both columns hold the same numeric unique identifier for each Ontario Public Health Unit. PHU_ID is also a foreign key for "Ministry of Health Public Health Unit Boundary". The tables will be joined using the PHU_NUM and PHU_IDs columns from both tables since they contain the same unique identifiers. Other foreign key assignments are: PHU_NAME in "Status of COVID-19 cases in Ontario by Public Health Unit (PHU)" and NAME_ENG in "Ministry of Health Public Health Unit Boundary".

Once data is merged, cleaned and preprocessed we hope use AWS and ProstreSQL to store and share data. 

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

![ML Flowchart](Pictures/ML_flowchart.png)

