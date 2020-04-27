# GA-DSI-Hackathon-Airbnb
### Nate Bukowski and Matt Burke

# Contents:
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Data Summary](#Data-Summary)
- [Models and Techniques](#Models-and-Techniques)
- [Conclusions](#Conclusions)

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

We also tried fitting KNN and SVM models, however, they timed out before 


# Data Summary
**Data Source:**
- The data for this project was scraped from Reddit using [Pushshift’s API](https://github.com/pushshift/api). [r/userexperience](https://www.reddit.com/r/userexperience/) and [r/UXResearch](https://www.reddit.com/r/UXResearch/) were the subreddits from which the text data was extracted.

**Datasets Analyzed:**
- [merged_processed.csv](./datasets/merged_processed.csv)
  -  13,611 rows, 2 columns


### Data Dictionary
|Feature|Type|Dataset|Description|
|--|--|--|--|
|**subreddit**|*nominal*|merged_processed|binary classification variable; 1=r/userexperience, 0=r/UXResearch|
|**text**|*string*|merged_processed|text from the subreddit post (submissions and comments)|


# Models and Techniques
- The goal was to find a classification model that performed best when classifying a subreddit post. *userexperience (1)*  was the positive class and *UXResearch (0)* the negative class. In order to do this I performed various tests on the following models:
  - Logistic Regression
  - Multinomial Naive Bayes
  - Random Forest
  - AdaBoost
  - Voting Classifier
- I used two vectorizers from sklearn:
  - CountVectorizer()
  - TfidfVectorizer()
- For each model, I tested various combinations hyperparameters for the respective vectorizers. To do this I set up pipelines with the transformers and estimators (e.g, CountVectorizer, Logistic Regression), tested various hyperparameters (e.g., stop words, n-gram range), and ran this through a GridSearch.
- Each model was then fit using training data.
- Both train and test datasets were scored using accuracy and evaluated against the baseline accuracy (53% positive class; 47% negative class).

# Conclusions
- *Model #4: Logistic Regression, TfidfVectorizer* performed best
  - Train accuracy score: 74%
  - Test accuracy score: 72%
  - Parameters:
    - `stopwords: 'english'` (native to sklearn)
    - `n-gram range: (1,2)`
    - `solver: liblinear`
    - `penalty: l1` (lasso regression)
  - Analysis:
    - Though 72% accuracy was not the best across all test sets, it was the closest to that of the train set. For other models, I was getting test scores at least 20 percentage points less than those of train scores.
    - Therefore, I selected this model as the best as it would perform most closely with expectations on unseen data.
    - The most notable hyperparameter adjustment was changing the penalty from the default `l2` (ridge regression) to `l1` (lasso regression). All else held equal, the train/test respectively scored 92.3%/75.6% accuracy using the `l1` penalty. Allowing the coefficients to zero out using `l2` makes the train/test accuracy scores more consistent with one another.
- Though I would have liked to see a higher accuracy score in my best model, a 72% accuracy isn't bad considering how closely related the subreddits of choice were. Compared to the baseline accuracy (53% positive class) my best model performed 19 percentage points higher.
- The largest challenge with this project was computing constraints. Given the complexity of some of the models and their hyperparameters, my computer wasn't able to process everything. For example, when I tried to compare the `elasticnet` and `l1` hyperparameters for Logistic Regression, my computer ran for 20+ minutes before the Jupyter kernel froze. Given sufficient time and computing resources, I believe I could continue tuning the models to get an accuracy score well above 72%.


**Next Steps**
- Before putting this model into any sort of production, the accuracy scores would need to be increased by at least 15 percentage points. To that end, next steps would be acquiring more computing power and testing multiple hyperparameters (e.g., different stopwords, n-grams, penalities, etc) over various models. Upon training a model with a sufficient accuracy score, a few interesting implementations of it might include analyzing posts to recommend posting in the other subreddit in order to get more interaction or analyzing post quality to make recommendations to employers for potential candidates. These are just a few ideas that, especially when paired with other features from the API (e.g., time of post, number of upvotes), could lead to some very interesting insights. Before any idea is to be implemented, though, the accuracy score must improve.
