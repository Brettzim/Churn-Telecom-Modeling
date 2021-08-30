# Churn Telecom Modeling Project

<img src=https://www.surveyworksaustin.com/wp-content/uploads/2019/02/cell-tower-title-review-survey.jpg width="700" height="300">

Phase 3 Flatiron project developing ML models and predictions for SyriaTel

**Authors**: Nate Walter, Brett Zimmerman, Jax Garnett




## Table of Contents
* [Overview](#Project-Overview)
* [Business Problem](#Business-Problem)
* [The Data](#The-Data)
* [Data Cleaning](#Data-Cleaning)
* [Analysis](#Analyis)
* [Conclusions](#Conclusion)
* [Repository Structure](#Repository-Structure)

## Structure
```
.
├── Pitch.pdf
├── README.md
├── Syriatel_model_notebook.ipynb
└── data
    └── churn-data-set.csv
```


<img src=https://www.logolynx.com/images/logolynx/f7/f75fdb74aaa4f44040e65f7ed4a0952f.jpeg width="400" height="150">


## Project Overview
This repository analyzes the data on SyriaTel’s customer churn to create machine learning classification models capable of predicting if a customer will churn or not. Our objective is to create a model using the customer churn data in SyriaTels’ customer database. The goal of our model is to have a high F1 score and Recall scores, so we know that our predictions are meaningful to the situation. By using different machine learning techniques, we were able to identify if a customer will churn, making our model a useful tool for the phone company interested in allocating its resources to customers. 


 
## Business Problem
We are an independent company audit firm hired by SyriaTel to investigate opportunities to increase customer retention by predicting customer loss from analyzing past data. We aim to provide a model highly successful at identifying if a customer will end their relationship with SyriaTel. The company can then take actionable steps to reduce their deficit.

## The Data
This project uses the SyriaTel Customer Churn dataset. The dataset includes customers that do business with SyriaTel in all 50 states. The descriptions of the dataset's columns are shown below.

* State - a State abbreviation. The state location of the customer.
* Account Length - How long the customer has been with the company.
* Area code - Area code of the customer.
* Phone number - Phone number of the customer.
* International plan - true if the user has the international plan, otherwise false.
* Voicemail plan - true if the user has the voicemail plan, otherwise false.
* Number vmail messages - the number of voicemail messages the customer has sent.
* Total day minutes - total number of minutes the user has been in calls during the day.
* Total day calls - total number of calls the user has done during the day.
* Total day charge - total amount of money the user was charged by the Telecom company for calls during the day.
* Total eve minutes - total number of minutes the user has been in calls during the evening.
* Total eve calls - total number of calls the user has done during the evening.
* Total eve charge - total amount of money the user was charged by the Telecom company for calls during the evening.
* Total night minutes - total number of minutes the user has been in calls during the night.
* Total night calls - total number of calls the user has done during the night.
* Total night charge - total amount of money the user was charged by the Telecom company for calls during the night.
* Total intl minutes - total number of minutes the user has been in international calls.
* Total intl calls - total number of international calls the user has done.
* Total intl charge - total amount of money the user was charged by the Telecom company for international calls.
* Customer service calls - number of customer service calls the user has done.
* Churn - true if the user terminated the contract, otherwise false.

## Data Cleaning

The data here started out with no null values, and data types that aligned with the supposed data values. After some correlation analysis, we decided to remove all columns related to charge, as it was almost a 1:1 correlation with minutes. We also removed the “phone number” and “number vmail messages” columns. In order to turn the object columns into usable numerical data, we used a label encoder on the “Voice mail plan”, “International plan”, and “Churn” columns as they were binary values. We then One Hot Encoded the “State” column. Leaving us with uncorrelated numerical data.

## Analysis

We first created our baseline model with a dummy regressor.  Due to our large target class imbalance, we set the dummy to use the stratified strategy.
Since we planned on testing multiple models, we cut down the run time by creating functions that fit a model in a pipeline, and ran it giving us the train and test metrics and scores. The metrics we focused on were maximizing the Recall and F1 scores. 

Our first simple model was a Logistic Regression model. It returned decent scores, but its main purpose was to be compared to other models we were more confident could end up being our final choice. So, we moved on to a Decision Tree. Tweaking the hyper-parameters on that led to some high scoring metrics. We chose them by agreeing to keep the max depth and sample splitting low, and then finding which values worked best. Our F1 and Recall scores were improving, showing that we were on the right path to making accurate predictions with our models.  With this encouragement, we then moved on to a Random Forest Classifier. Not getting the precise results we wanted, we plugged the Random Forest into a Grid Search to find the best parameters. This technique proved successful, yet again, bringing our Test F1 and Recall scores to their highest levels yet. However, we wanted to combine the best attributes of all of the models into one, and this is where stacking comes in.

Stacking is the best approach because it combines the results of multiple models being run concurrently and feeds those results into the next set of models which, in turn feed into the final Logistic Regression model. This technique produced our best F1 and Recall scores, making it the final predictor.

## Conclusion

When creating predictive machine learning models, being experimental with the models can produce results approaching absolute certainty. Our iterative process brought us to a complex stacking algorithm that produced the best predictive results on whether a SyriaTel customer will churn or not.  
