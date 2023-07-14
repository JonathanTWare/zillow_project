# <a name="top"></a>Zillow Project - Predicting Property Tax Assessed Values 
![]()


***
[[Project Description](#project_description)]
[[Project Planning](#planning)]
[[Key Findings](#findings)]
[[Data Dictionary](#dictionary)]
[[Data Acquire and Prep](#wrangle)]
[[Data Exploration](#explore)]
[[Statistical Analysis](#stats)]
[[Modeling](#model)]
[[Conclusion](#conclusion)]
___



## <a name="project_description"></a>Project Description:

In this project we will be using the Telco Data Set. Exploring the data, we will find features that are correlated with Property Tax Assesed Values (taxvaluedollarcnt)using PearsonsR, in order to run features through a model that will predict the Property Tax Assessed Values. The goal is to beat baseline using one of the four regression models: Linear Regression(OLS), LassoLars, TweedieRegressor(GLM), and Polynomial Regression.

[[Back to top](#top)]

***
## <a name="planning"></a>Project Planning: 
[[Back to top](#top)]


### Objective

Find out what the home value will be by utilizing four algorythms and running the best scoring algrothym on test score.



### Target variable
The target variable of this project is tax_value.


### Need to haves (Deliverables):
-Need to explore the data.
-Run features through statistical tests.
-Select features for modeling
-Run features through 3 different algorythms.



### Nice to haves (With more time):
Further feature explore to see if error can be further improved.


***

## <a name="findings"></a>Key Findings:
- square feet was correlated with the home's value.
- The County Code was had a very weak correlation with the home value.
- bathroom count and square feet had the strongest correlation out of all features.

[[Back to top](#top)]


 

***

## <a name="dictionary"></a>Data Dictionary  
[[Back to top](#top)]

### Data Used
---
| Attribute | Definition | Data Type |
| ----- | ----- | ----- |
| bathroom_count | the amount of bathrooms in the home| float |
| bedroom_count|the amount of bedrooms in the home | float |
| calc_sqr_feet |the calculated square footage of the home|float |
| tax_value |the home's value ($) | float |
| county_code |the county code of the property |  float
**

## <a name="wrangle"></a>Data Acquisition and Preparation
[[Back to top](#top)]

![]()


### Wrangle steps: 
- renamed columns to be more readable:

|original name| rename|
| ---- | ---- |
|bedroomcnt| bedroom_count|
|bathroomcnt| bathroom_count|
|calculatedfinishedsquarefeet | calc_sqr_feet|
|taxvaluedollarcnt|tax_value|
|fips | county_code|
- dropped unwanted columns.
- created dummies for certain features
- created function to acquire and prep data
-function created to scale certain features


*********************

## <a name="explore"></a>Data Exploration:
[[Back to top](#top)]
- Python files used for exploration:
    - wrangle.py
    - explore.py
    
    


### Takeaways from exploration:
- Five features were chosen for statistical testing: bathroom count, bedroom count, calculated square feet, county code, and year built


***

## <a name="stats"></a>Statistical Analysis
[[Back to top](#top)]

### Stats Test 1: Pearson's R

Pearson's correlation coefficient (Pearson's R) is a statistical measure used to assess the strength and direction of the linear relationship between two continuous variables.

By calculating Pearson's R, we aim to determine whether there is a significant linear association between the independent variable and the dependent variable. The coefficient helps us quantify the extent to which the variables vary together and provides insight into the direction (positive or negative) and strength (magnitude) of the relationship.

To calculate Pearson's R in Python, we can use the corrcoef function from the numpy module. This function takes the two variables as input and returns the correlation matrix, where the coefficient of interest is the element in the [0, 1] or [1, 0] position. Pearson's R ranges from -1 to 1, where -1 indicates a perfect negative linear relationship, 0 indicates no linear relationship, and 1 indicates a perfect positive linear relationship.


### Hypothesis

In summary, the hypotheses for the PearsonsR test can be stated as follows:

### 1st Hypothesis

Null Hypothesis (H0): bathroom_count does not have a correlation with tax_value.
Alternative Hypothesis (H1): bathroom_count has a correlation with tax_value.

### 2nd Hypothesis

Null Hypothesis (H0): bedroom_count does not have a correlation with tax_value.
Alternative Hypothesis (H1): bedroom_count has a correlation with tax_value.

### 3rd Hypothesis

Null Hypothesis (H0): yearbuilt does not have a correlation with tax_value.
Alternative Hypothesis (H1): yearbuilt has a correlation with tax_value.

### 4th Hypothesis

Null Hypothesis (H0): calc_sqr_ft does not have a correlation with tax_value.
Alternative Hypothesis (H1): calc_sqr_ft has a correlation with tax_value.


### Stats Test 1: Independent T=Test

The independent t-test is a statistical method used to examine the association between a categorical variable and a continuous variable.

By using the independent t-test, we aim to determine whether there is a significant association between the both one categorical variable and a continuous variable. 


### 5th Hypothesis

Null Hypothesis (H0): county_code is not associated with tax_value.
Alternative Hypothesis (H1): county_codeis associated with tax_value.


#### Confidence level and alpha value:
- I established a 95% confidence level
- alpha = 1 - confidence, therefore alpha is 0.05

#### Results:

| Feature | P-Value | Corellation Value | Correlation Strength|
| ---- | ---- | ---- | ---- |
| bathroom_count| 0 |0.40  |moderate |
| bedroom_count|1.41e-71 |0.12 |weak |
| calc_sqr_ft|0 |0.48  | moderate |
| yearbuilt | 1.31e-23 |0.07      |  weak     |

| Feature | P-Value Value |
| ---- | ---- |
| county_code | 0 |


#### Summary: 
bathroom_count and calc_sqr_ft have a moderate correlation with the target(tax_value). However, yearbuilt, bedroom_count and the county code dummies have a very week correlation with the target.




***

## <a name="model"></a>Modeling:
[[Back to top](#top)]


### Baseline
    
- Baseline Results: 

| Model | Train Score | 
| ---- | ---- | 
| Baseline |$433,865.92 | 

- Selected features to input into models:
    - features = bathroom_count, bedroom_count, calc_sqr_ft, yearbuilt, and all encoded county codes.

***

### Models

    
#### Model 1: Linear Regression (OLS)



##### The OLS model had a train RMSE of 369926.63 which was 15% better than baseline, a validation RMSE of 364517.28



### Model 2 : LassoLars


 
##### The LassoLars model  had a train RMSE of 369926.65 which was 15% better than baseline, a validation RMSE of 364515.70



### Model 3 : TweedieRegressor (GLM)



##### The GLM model  had a train RMSE of 408563.89 which was 6% better than baseline, a validation RMSE of 403213.88



### Model 4 : Polynomial Regression



##### The Polynomial Regression model  had a train RMSE of 359127.93 which was 17% better than baseline, a validation RMSE of 354205.71



## Selecting the Best Model:

### Use Table below as a template for all Modeling results for easy comparison:

|model |	RMSE_train |	RMSE_validate	| R_Validate|
| ---- | ----| ---- | ---- | 
|mean_baseline|	433865.92|	428222.25|	0.000000	|
|OLS	|369926.63	|364517.28|	0.275380|
|LassoLars	|369926.65	|364515.70|	0.275386|	
|GLM	|408563.89	|403213.88	|0.114239|	
|POLY	|359127.93	|354205.71|	0.315790|



##### Polynomial Regression preformed best


## Testing the Model

- Model Testing Results

|model |	RMSE_train |	RMSE_validate	| RMSE_test |
| ---- | ----| ---- | ---- | 
|Poly| 359127.93 | 354205.71 | 357684.12|  



***

## <a name="conclusion"></a>Conclusion:

#### Based on the information provided, it seems that the Polynomial Regression model has the lowest RMSE at 35,9127.93 , which is 18% better than baseline. 
#### 
#### On the other hand, the LassoLars and Linear Regression models had a slightly lower error reduction at 15% better than baseline.
#### 
#### The TweedieRegressor model barely outperformed baseline by 6%.
#### 
#### Considering all models, as they did all beat baseline, Polynomial Regression model outperformed baseline by 17% which was the highest in error reduction.
####
#### After running the Polynomial Regression model, a test score of  was given 357,684.12 which was 18% over baseline.

[[Back to top](#top)]