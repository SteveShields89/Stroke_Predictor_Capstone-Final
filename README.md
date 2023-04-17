## Problem Statement:
   Lotus Bioinformatics (LBI) is a company that has been tasked by the VA to help create a prediction model for strokes. Every year more than 790,000 people have a stroke, of that number, there about 600,000 that are having a stroke for the first time. According to the CDC, in 2020, 1 in 6 deaths from cardiovascular disease was to due stroke. Would it not be worthwhile to try and build model that may help to mitigate those deaths. To help and provide some type of early warning system for those who are suffering from pooor health. That is where LBI comes in. 
    Through vigorous research, we have found multiple data sets to help up us solve this problem or at least attempt.

## Data Dictionary and Description:
   The data set that was used was one found on Kaggle. There were a little under 50,000 observations with 12 columns. After some cleaning and engineering we ended up with 18 columns. Listed below are the columns used with out one hot encoding.

   |Feature|Type|Description|
   |---|---|---|
   |age|int64|participants age|
   |hypertension|int64|0 for no hypertension and  1 for hypertension|
   |heart_disease|int64|0 for no heart disease and 1 for heart disease|
   |avg_glucose_level|int64|Glucose test done 2-3 hrs after glucose consumption |
   |bmi|int64|Number based on weight and height|
   |stroke|int64|0 for no stroke  and 1 for stroke (target)|
   |diabetes|int64|0 for no diabetes and 1 for diabetes|
   |smoking_status|object|Never Smoked, Fomerly Smoked,Smokes, Unknown|
   |ever_married|object|Yes or No|
   |work_type|object|Self employes, Private, Children, or Never Worked|
   |residence_type|object|Rural or Urban|
   |gender|object|Male,Female, or Other|

    

   
## Data Cleaning and Model Selection:
   The data cleaning started off with handling null values in the smoking status column.I decided to map the NaN values to never smoked. On forms that people filled out there was probably an N/A or they just did not answer because they do not smoke. I then decided to handle the values of the bmi column. In the process of trying to decide what to do with the nulls, I saw some outliers. As a health professional, a 97.6 bmi is improbable. BMI usually tops out at ~45-55. A BMI of 40 is already extreme obesity so there is really no need to use the metric past that, as it won't give you any more detail. Waist to Hip ratio would be a better metric to use in such cases. In order to handle those outliers, I made a loop to iterate over the column and any values above 70 were multiplied by .1 making them low single digit/double digit numbers. After that I changed any null values to the mean of all bmi's which was around 28.6.I then went on to EDA since I felt satisified with those results.
    For EDA, I looked at multiple relationships between variables. I looked at the counts for diabetes present, hypertension, those who have had strokes, those with hypertension, and heart disease. I have added some of those below:
     
  ![Scatter of BMI and Age](http://localhost:8890/view/Stroke%20Predictor%20-%20Capstone/img/age_bmi_scatter.png)
  ![Hypertension](http://localhost:8890/view/Stroke%20Predictor%20-%20Capstone/img/hypertension.png)
  ![AVG glucose and BMI](http://localhost:8890/view/Stroke%20Predictor%20-%20Capstone/img/avg_glucose_and_bmi.png)
  ![Stroke proportion](http://localhost:8890/view/Stroke%20Predictor%20-%20Capstone/img/stroke_prop.png)
    
   Finally,after one hot encoding our categorical variables, we went on to modeling. The modeling process was straight forward. I created a list of dictionaries with each classification model I wanted to use and made a loop using gridsearch to go through all of the models.After all the models had run, we looked at the accuracy to determine which one is the best for our chosen metric of success. To note, the baseline score was .978. Using the baseline, these models performed the best:

   1. Bagging Trees - .9857 acc
   2. Logistic Regression - .979 acc
   3. Gradient Booost - .9869 acc
   
   In all of these models there were over 7000 properly predicted true negatives. Gradient boosr properly predicted 63 true positives and Bagging Trees properly predicted 45. Bagging trees however, had 103 false negatives as opposed to the Gradient Boost's 85. In order to move forward with a production model, I would like to see the false negatives be a lot lower. More data would be needed for that and maybe more parameter tuning to mitigate these false negatives. The goal is to help people to predict strokes and not give them a false sense of security when could potentially face a life threatening stroke. 
    
## Conclusion/Next Steps:

   We plan on eventually moving forward with one of these models but would a few million more observations to feel confident enough to put any of them in to production. We will continue to gather and clean data to accomplish this goal, and with the help of the CDC and maybe WHO, we can have a production model ready by the end of the year.


## Sources: 
 https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset
 
 https://www.cdc.gov/stroke/about.htm
 
