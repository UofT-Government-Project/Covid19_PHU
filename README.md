
## Machine Learning- Week2

### The Machine learning model based o the new dataset:
LogisticRegression from ML sklearn library

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
-Set active Covid cases as our target(y)
-Removed three columns ( active cases, fatal cases and resoved cases) from our dataframe to set up our features (X)

### Training and testing set:  
-Split our data into training and testing by train_test_split function from sklearn library
-Scaled the data
### Logistic Regression ML model:
 -Accuracy score 0.977

### Reasons for using Logistic Regression:

-It is a classification algorithm analyzes continues and categorial variables.
-It generates relatively high accuracy score while it is a straightforward model , easy to implement and interpret.
-LR makes no asuumptions about classes in features and it is fast at classifying unknown records. 
-It predicts probability of high covid cases in public health units (PHU) in Ontario. 


### Limitations:

- Logistic regression model assumes linearity between the dependent variable and independant variables
- Non-linear problems can not be solved with this model
- It is difficult to get complex relationships with this model and deep learning Neural Networks can outperfom LR model.


  


