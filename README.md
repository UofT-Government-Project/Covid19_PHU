# Covid-19 and Public Health Units in Ontario

## Communication protocol
A group chat has been set up in Slack.  This will be the primary platform for ongoing correspondence by each team member while working on our individual roles for each segment.  Every Monday and Wednesday evenings will be an opportunity to meet via zoom and discussing the current week's agenda.  Every Sunday the team will connect via Google Meet as well to finalize the submission of the current week.  Additional meetings will be set up throughout the week when needed.<br>
Phone numbers have been exchanged and a group chat set up on WhatsApp for ad hoc communications as well. <br>
*Collaborators:* [Lida](https://github.com/lidajav), [Tarana](https://github.com/taranahassan), [Michelle](https://github.com/MichelleGoldfinger), [Blessing](https://github.com/Physsyb), [Faridah](https://github.com/faridah-m).

### Team Member roles:
***Tarana:***  Setting up repository, branches and updating README.md.<br>
***Faridah:***  Explanation of the ETL process on data.<br>
***Michelle:***  Creating an ERD for the mockup database to be used.<br>
***Lida:*** Creating the mockup machine learning model to be used. <br>
***Blessing:***  Explanation of which technologies group will be using and why.

## Extract, Transform & Load

Two sets of data have been used for the machine learning model; these datasets will be providing a prediction of which Public Health Unit(s) may have a potential risk of higher active cases. We have been tasked with combining these two datasets, cleaning the data so that all participants can use the final combined dataset and finally saving the data into a PostgreSQL database.

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

ERD PIC

The first table PHU_Locations contains the following columns: id, PHU_id (primary key), Reporting_PHU, Reporting_PHU_Address, Reporting_PHU_Latitude and PHU_Longitude. The second table PHU has the following columns: id (primary key), age_group, gender, outcome, outbreak, phu_id (foreign key), week, month, year. The columns for the third table, PHU_Gender_final are: index, phu_id (foreign key), gender, gender_count. Lastly, the fourth table called PHU_Age_Group_Final contains the following columns: index, phu_id (foreign key) and age_group_count.

## Database Storage
A database instance was created on AWS’ RDS and buckets were created on AWS’ S3 to hold all four tables.

<img width="1082" alt="AWS RDS" src="https://user-images.githubusercontent.com/75905911/119559642-f2a7c480-bd70-11eb-81bd-8575e47d3c99.png">

<img width="1110" alt="AWS S3" src="https://user-images.githubusercontent.com/75905911/119559660-f9ced280-bd70-11eb-9c77-85b4c9e519b5.png">

## Connection String
To connect our database, we used SQLAlchemy’s create engine

<img width="1381" alt="Connection String" src="https://user-images.githubusercontent.com/75905911/119559713-09e6b200-bd71-11eb-959b-462f747fbfcf.png">


<img width="1067" alt="phu" src="https://user-images.githubusercontent.com/75905911/119559764-179c3780-bd71-11eb-8609-e19609139ea0.png">
<img width="495" alt="phu_age_group_final" src="https://user-images.githubusercontent.com/75905911/119559766-18cd6480-bd71-11eb-97f9-8d796569b7ea.png">
<img width="474" alt="phu_gender_final" src="https://user-images.githubusercontent.com/75905911/119559769-1965fb00-bd71-11eb-870b-4902914dda97.png">
## pgAdmin Database
Our four tables and their corresponding data were imported to pgAdmin.
The following is our sql for table creation:

--Create PHU_locations table
CREATE TABLE PHU_locations (
    id INT,
    PHU_id INT,
    Reporting_PHU VARCHAR,
    Reporting_PHU_Address VARCHAR,
    Reporting_PHU_Latitude FLOAT,
    Reporting_PHU_Longitude FLOAT,
    PRIMARY KEY(PHU_id)
);

--Create PHU table
CREATE TABLE PHU (
    id INT,
    age_group VARCHAR,
    gender VARCHAR,
    outcome VARCHAR,
    outbreak VARCHAR,
    phu_id INT,
    week INT,
    month INT,
    year INT,
    PRIMARY KEY (id),
    FOREIGN KEY (phu_id) REFERENCES PHU_locations (PHU_id)
);

--Create PHU_Gender_Final table
CREATE TABLE PHU_Gender_Final (
    index INT,
    phu_id INT,
    gender VARCHAR,
    gender_count INT,
    FOREIGN KEY (phu_id) REFERENCES PHU_locations (PHU_id)
);


--Create PHU_Age_Group_Final table
CREATE TABLE PHU_Age_Group_Final (
    index INT,
    phu_id INT,
    age_group VARCHAR,
    age_group_count INT,
    FOREIGN KEY (phu_id) REFERENCES PHU_locations (PHU_id)
);

And images for our tables with data:

<img width="1067" alt="phu" src="https://user-images.githubusercontent.com/75905911/119559821-2aaf0780-bd71-11eb-81a4-6d1cfcb17753.png">
<img width="495" alt="phu_age_group_final" src="https://user-images.githubusercontent.com/75905911/119559835-2da9f800-bd71-11eb-96ea-424241034d8e.png">
<img width="474" alt="phu_gender_final" src="https://user-images.githubusercontent.com/75905911/119559849-30a4e880-bd71-11eb-8b03-d13f02aeb44c.png">
<img width="926" alt="PHU_locations" src="https://user-images.githubusercontent.com/75905911/119559854-33074280-bd71-11eb-9329-b5cf19da85fb.png">

## pgAdmin Table Join
Our last and 5th table was created using an sql inner join of all four tables. The SQL code is here:

---Joining all four tables
SELECT phu_locations.id, 
    phu_locations.phu_id, 
    phu_locations.Reporting_PHU,
    phu_locations.reporting_phu_address, 
    phu_locations.reporting_phu_latitude, 
    phu_locations.reporting_phu_longitude, 
    phu.outcome,    
    phu.outbreak, 
    phu.week, 
    phu.month, 
    phu.year, 
    phu_age_group_final.age_group, 
    phu_age_group_final.age_group_count, 
    phu_gender_final.gender, 
    phu_gender_final.gender_count 
INTO phu_joined
FROM phu_locations
INNER JOIN phu ON phu_locations.id = phu.id
INNER JOIN phu_age_group_final ON phu_locations.phu_id = phu_age_group_final.phu_id
INNER JOIN phu_gender_final ON phu_locations.phu_id = phu_gender_final.phu_id


And an image of the table with the data can be seen here:
<img width="1141" alt="phu_joined1" src="https://user-images.githubusercontent.com/75905911/119559938-50d4a780-bd71-11eb-9279-8930bb3c4b1a.png">
<img width="1146" alt="phu_joined2" src="https://user-images.githubusercontent.com/75905911/119559952-53370180-bd71-11eb-93ee-719e319c66e4.png">



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



