
## Machine Learning- Week2

### The Machine learning model based on the new dataset:
RandomForest Classifier from ML sklearn library

### Based on the new dataset,our prediction is the fatal cases of covid cases.The dataset lacks continues features that have an impact on our predications. 
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

### Set the Target and features
- Removed ' Not recivered' from outcome so we end up with two classes 'Fatal' and 'Recovered'
- Set Fatal cases as our target(y)
- Removed three columns ( fatal cases and resolved cases) from our dataframe to set up our features (X)

### Training and testing set:  
- Split our data into training and testing by train_test_split function from sklearn library
- Scaled the data
### RandomForest Classifier ML model:
- Accuracy score 0.92 - The high accuracy is due to high recovery rate of covid.


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


  


