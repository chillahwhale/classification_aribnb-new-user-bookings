# Project Summary
### Nate Bukowski and Matt Burke

# Contents:
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Data Summary](#Data-Summary)
- [Models and Techniques](#Models-and-Techniques)
- [Next Steps](#Next-Steps)

# Problem Statement
Predict in which country a new user will make his or her first booking. This project is based on the Kaggle competition [Airbnb New User Bookings](https://www.kaggle.com/c/airbnb-recruiting-new-user-bookings). 

# Executive Summary
For this Hackathon project we had 7.5 hours to select 1 of 11 Kaggle competition project, complete it, then present our finding. We selected Airbnb New User Bookings, a classification problem to predict in which country a new user will make his or her first booking. 

There were 12 possible country outcomes: There are 12 possible outcomes of the destination country: 'US', 'FR', 'CA', 'GB', 'ES', 'IT', 'PT', 'NL','DE', 'AU', 'NDF' , and 'other'; ‘NDF’ represents a user that did not end up bookingand ‘other a user that ended up booking but in a country not included on the list. After completing basic data cleaning (e.g., treating NaNs and deleting extraneous features) we performed basic feature engineering, such as creating dummies for categorical variables. The vast majority of observations fell in either US (39.1%) or NDF (44.7%).

Below are the accuracy scores for the best performing models:
- **Random Forest:**
  - Train accuracy: 94.7% 
  - Test accuracy: 77.5%
  
- **Logistic Regression:**
  - Train accuracy: 83.903% 
  - Test accuracy: 83.898%

We also tried fitting kNN and SVM models, however, both models were still fitting by the time we needed to present our findings.

Given more time, we would have liked to do the following:
- Additional feature engineering, including interaction terms and stacking
- Continue to tweak the Logistic Regression hyperparameters
- Fit alternative models such as kNN and SVM 

# Data Summary
**Data Source:**
- The data for this project was pulled from [Kaggle competition page](https://www.kaggle.com/c/airbnb-recruiting-new-user-bookings/data). 

**Datasets Analyzed:**
- [train_cleaned.csv](./datasets/train_cleaned.csv)
  -  120,719 rows, 140 columns

# Models and Techniques
- The goal was to find a classification model that performed best when classifying a subreddit post. *userexperience (1)*  was the positive class and *UXResearch (0)* the negative class. In order to do this I performed various tests on the following models:
  - Logistic Regression
  - Random Forest

- For each model, I tested various combinations hyperparameters for the respective vectorizers. To do this I set up pipelines with the transformers and estimators (e.g, CountVectorizer, Logistic Regression), tested various hyperparameters (e.g., stop words, n-gram range), and ran this through a GridSearch.
- Each model was then fit using training data.
- Both train and test datasets were scored using accuracy and evaluated against the baseline accuracy (53% positive class; 47% negative class).


**Next Steps**
Given more time, we would have liked to do the following:
- Additional feature engineering, including interaction terms and stacking
- Continue to tweak the Logistic Regression hyperparameters
- Fit alternative models such as kNN and SVM 

