# MultipleLinearRegression

## Table of contents:

  - Load Data
  - Dataset Cleaning
  - Data Visualization
  - Data Preaparation
  - Dummy Variables
  - Splitting the Data into Training and Testing
  - Rescaling of Features
  - Building our model using Recursive feature elimination (RFE)
  - VIF Calculation
  - Dropping the variables
  - Residual Analysis of the train data
  - Making Predictions
    
    
### 1. Load Data:
First of all we just loaded the libraries and then loaded the dataset.

### 2. Dataset Cleaning:
There were no missing values in the dataset.
'dteday' was dropped because 'yr', 'month', 'weekday' were present in the dataset
'casual' and 'registered' are dropped because'cnt' is there in the dataset that is the sum of both.
'instant' is dropped because it is nothing but index, so it will not impact on 'cnt'.

### 3. Data Visualization:
After that visualization of continuous variablesis are done by plotting the pairplot. From the pairplot, it can be seen that 'temp' and 'atemp' is more correlated with 'cnt'.

### 4. Data Preparation:
Now it can be seen that some of the variables are having more than two levels. So we have to create dummy variables for them. To do so, those variables are converted into Categorical Variables. List of the variables that are having more than two levels are:

- Season :
'season' is mapped as follows: 

A. 1:spring

B. 2:summer

C. 3:fall

D. 4:winter

- weathersit:
'weathersit' is mapped as follows:

A. 1: Clear, Few clouds, Partly cloudy, Partly cloudy = clear

B. 2: Mist + Cloudy, Mist + Broken clouds, Mist + Few clouds, Mist = Few clouds

C. 3: Light Snow, Light Rain + Thunderstorm + Scattered clouds, Light Rain + Scattered clouds = Scattered Clouds

D. 4: Heavy Rain + Ice Pallets + Thunderstorm + Mist, Snow + Fog = Thunderstorm

- weekday:
'weekday' is mapped as follows:

A. 0: "Sun"

B. 1: "Mon"

C. 2: "Tue"

D. 3: "Wed"

E. 4: "Thu"

F. 5:"Fri"

G. 6:"Sat"

- mnth:
'mnth' is mapped as follows:

A. 1: "Jan"

B. 2: "Feb"

C. 3: "Mar"

D. 4: "Apr"

E. 5: "May"

F. 6: "Jun"

G. 7: "Jul"

H. 8: "Aug"

I. 9: "Sept"

J. 10: "Oct"

K. 11: "Nov"

L. 12: "Dec"

After that mapping, Barplot for all the categorical variables are plot with respect to 'cnt'. and it can be seen from the bar plot that when season is fall and weather is clear, cnt is significantly higher.

### 5.Dummy Variables:
After that, Dummy variables for all the categorical variable that are having more than two levels are added. and the first dummy variable for all the features are dropped because they were not needed. And after dropping them, we concatenate those dummy variables with the original dataset.
After That we dropped the original feature because we have created dummy variables for them.

### 6. Splitting the Data into Training and Testing:
After that, data is splitted into training and testing. Here 70% data is splitted into training set and 30% of data will be there for testing purpose.

### 7. Feature Scaling:
Scaling of some features are done here except dummy variables and 0-1 variables, because they have pretty much higher values that can dominate other features.

Here We are using MinMaxScalar, that converts all the values in between 0 - 1.

The features for which scaaling is performed are as follows:

- temp
- atemp
- hum
- windspeed
- cnt

### 8. Building our model using Recursive feature elimination (RFE):

Here RFE is used to select features. Both automatic and manual methods are applied to select the features. First of all, 15 features are selected randomly by RFE method and then the summary is described. Then we got the P-value for all the features that are randomly selected and R2  score and adjusted R2 score is also calculated. To eliminate the feature p-value will not be sufficient. So next step is followed.

### 9. VIF Calculation:
VIF is calculated for all the features to drop the variables. Feature that are having greater than 5.0 VIF, will be eligible to get dropped.

### 10. Dropping the variables:
So, there will be variables that have p-value and VIF..So what feature shall be dropped? Some rules are followed:

- High p-value & High VIF: that should be dropped first
- Low p-value & Low VIF: keeping those variables 
- High p-value & Low VIF: Remove them secondly
- Low p-value & High VIF: remove them thirdly

the variables are dropped one by one and after each variable drop, a model is built and P-value, VIF, R2 score and Adjusted R2 score is calculated till we will get VIF that is less than 5 and lesser p-value for each feature.

### 11. Residual Analysis of the train data:
The graph is plot for the error terms and it can be seen that error terms are normally distributed i.e. mean of the errors are zero. It should be like that because this is the assumption of Linear Regression.

### 12. Making Predictions:
At Last predictions are made on the test sset and R2 score is calculated. here, our Model is having r2 score as 0.824 for training set and 0.804 for our test set.

Equation of our Model will be :

(0.24 * yr) – (0.97 * holiday) + (0.41 * temp) – (0.14 * windspeed) – (0.12 * spring) + (0.05 * winter) – (0.08 * Few Clouds) – (0.29 * scattered clouds) + (0.07 * Sept)

