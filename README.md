# Credit-card-approval-prediction
Built a machine learning model to predict credit card approval without affecting users’ credit scores by avoiding hard inquiries. Performed EDA, correlation analysis, and model training, selecting Gradient Boosting with recall as the key metric. Deployed the model using AWS S3

Key findings: People with the highest income, and who have at least one partner, are more likely to be approved for a credit card.

## Data source

- [Kaggle credit card approval prediction](https://www.kaggle.com/rikdifos/credit-card-approval-prediction)

## Methods

- Exploratory data analysis
- Bivariate analysis
- Multivarate correlation
- S3 bucket model hosting
- Model deployment
## Tech Stack

- Python (refer to requirement.txt for the packages used in this project)
- Streamlit (interface for the model)
- AWS S3 (model storage)


## Quick glance at the results

Top 3 models (with default parameters)

| Model     	                | Recall score 	|
|-------------------	        |------------------	|
| Support vector machine     	| 88% 	            |
| Gradient boosting    	        | 90% 	            |
| Adaboost               	    | 79% 	            |


- ***The final model used is: Gradient boosting***
- ***Metrics used: Recall***
- Why choose precision as metrics:
  Since the objective of this problem is to minimize the risk of credit default for the financial institution, the metrics to use depends on the current economical situation:

  - During the time of a bull market (when the economy is expending), people feel wealthy and usually are employed. Money is usually cheap and the risk of default is low. The financial institution is able to handle the risk of default therefore is not very strict on giving out credit. The financial institution can handle a number of bad clients as long as the vast majority of applicants are good clients (aka those who payback their credit).In this case, having a good recall (sensitivity) is ideal.
  - During a bear market (when the economy is contracting), people loose their jobs and their money through the stock market. Many people struggle to meet their financial obligations. The financial institution therefore tend to be more conservative on giving out credit or loans. The financial institution can't afford to give out credit to clients who won't be able to pay back their credit. The financial institution would rather have a smaller number of good clients even if it means that some good clients where denied credit, and ideally not have any bad client. In this case, having a good precision (specificity) is desirable.

    Note: There is always a trade-off between precision and recall. Choosing the right metrics depends on the problem you are solving.

    Conclusion: In our case, since we are in the longest bull market (not including the March 2020 flash crash), we will use recall as our metric.


## Lessons learned and recommendation

- Based on the analysis on this project, we found out that the education level and type of relationship are the most predictive features to determine if someone makes more or less than 50K. Other features like Capital gain, hours work and age are also usefull. The least usefull features are: their occupation and the workclass they belong to.
- Recommendation would be to focus more on the most predictive feature when looking at the applicant profile, and pay less attention on their occupation and workclass.
## Limitation and what can be improved

- Speed: since the model is stored on AWS S3, it can take some few seconds to load. Solution: cache the model with the Streamlit @st.experimental_singleton for faster reload.
- Dataset used: the dataset used is from 1990, inflation has not been taken into consideration and the countries's economies have changed since then. Solution: retrain with a more recent dataset.
- Hyperparameter tuning: I used RandomeSearchCV to save time but could be improved by couple of % with GridSearchCV.


## Repository structure


```


├── datasets
│   ├── GDP.csv                     <- the data used to feature engineering/enriched the original data.
│   ├── test.csv                    <- the test data.
│   ├── train.csv                   <- the train data.
│
│
├── assets
│   ├── confusion_matrix.png        <- confusion matrix image used in the README.
│   ├── gif_streamlit.gif           <- gif file used in the README.
│   ├── heatmap.png                 <- heatmap image used in the README.
│   ├── Income_classification.png   <- banner image used in the README.
│   ├── environment.yml             <- list of all the dependencies with their versions(for conda environment).
│   ├── roc.png                     <- ROC image used in the README.
│
├── pandas_profile_file
│   ├── income_class_profile.html   <- exported panda profile html file.
│
│
├── .gitignore                      <- used to ignore certain folder and files that won't be commit to git.
│
│
├── Income_Classification.ipynb     <- main python notebook where all the analysis and modeling are done.
│
│
├── LICENSE                         <- license file.
│
│
├── income_class_st.py              <- file with the best model and best hyperparameter with streamlit component for rendering the interface.
│
│
├── README.md                       <- this readme file.
│
│
├── requirements.txt                <- list of all the dependencies with their versions(used for Streamlit ).

```

