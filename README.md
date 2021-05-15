# Covid19_PHU
## Database Mock-Up
Two data sources were used to create the ERD for our project. The first dataset is the "Status of COVID-19 cases in Ontario by Public Health Unit (PHU)". Columns' details are: _id, FILE_DATE, PHU_NAME, PHU_ID, ACTIVE_CASES, RESOLVED_CASES and DEATHS. The second dataset titled "Ministry of Health Public Health Unit Boundary" has the following columns: FID, OGF_ID, PHU_ID, NAME_ENG, NAME_FR, GEO_UPD_DT, EFF_DATE, Shape__Area, and Shape__Length.


## ERD
<img width="1334" alt="ERD_COVID19_PHU" src="https://user-images.githubusercontent.com/75905911/118364910-7dfeaa00-b568-11eb-8350-cfeb2b81240b.png">

Primary Keys for both tables are: PHU_ID. PHU_ID is also a foreign key for "Ministry of Health Public Health Unit Boundary". Both tables will be joined using the PHU_IDs columns from both tables. Other foreign key assignments are: PHU_NAME in "Status of COVID-19 cases in Ontario by Public Health Unit (PHU)" and NAME_ENG in "Ministry of Health Public Health Unit Boundary".

Once data is merged, cleaned and preprocessed we hope use AWS and ProstreSQL to store and share data. 
