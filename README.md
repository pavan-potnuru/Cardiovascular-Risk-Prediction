# **Cardiovascular Risk Prediction**



## **Abstract**
Cardiovascular diseases (CVDs) are a group of disorders of the heart and blood vessels. Cardiovascular diseases are very common these days due to the change in life style and poor eating habits. So, predicting the risk of cardiovascular disease for given person by analyzing his/her past and present medical data and habits can save them if they act early against the disease and take precautionary measures.


## **Introduction**
According to the World Health Organization (WHO), cardiovascular diseases are the leading cause of death globally. An estimated 17.9 million people died from CVDs in 2019, representing 32% of all global deaths. Of these deaths, 85% were due to heart attack and stroke. Most cardiovascular diseases can be prevented by addressing behavioral risk factors such as tobacco use, unhealthy diet and obesity, physical inactivity and harmful use of alcohol. It is important to detect cardiovascular disease as early as possible so that management with counseling and medicines can begin.


## Problem Statement
We are here to explore the cardiovascular risk dataset and build a model to predict whether a given person has a 10-year risk of getting a cardiovascular disease. The main goal of the project is to: Find factors and causes which increase the risk of cardiovascular disease in a person. Using the data provided, this paper aims to analyze the data to determine what variables are correlated with 10-year risk of cardiovascular disease.


## **EDA Summary:**
•	The dependent variable is unbalanced, with only ~15% of the patients who tested positive for CHD.

•	All the continuous variables are positively skewed except age (which is almost normally distributed)

•	Majority of the patients belong to the education level 1, followed by 2, 3, and 4 respectively.

•	There are more female patients compared to male patients.

•	Almost half the patients are smokers.

•	100 patients under the study are undertaking blood pressure medication.

•	22 patients under the study have experienced a stroke.

•	1069 patients have hypertension.

•	87 patients have diabetes.

•	The risk of CHD is higher for older patients than younger patients.

•	18%, 11%, 12%, 14% of the patients belonging to the education level 1, 2, 3, 4 respectively were eventually diagnosed with CHD.

•	Male patients have significantly higher risk of CHD (18%) than female patients (12%)

•	Patients who smoke have significantly higher risk of CHD (16%) than patients who don't smoke (13%)

•	Patients who take BP medicines have significantly higher risk of CHD (33%) than other patients (14%)

•	Patients who had experienced a stroke in their life have significantly higher risk of CHD (45%) than other patients (14%)

•	Hypertensive patients have significantly higher risk of CHD (23%) than other patients (11%)

•	Diabetic patients have significantly higher risk of CHD (37%) than other patients (14%)

•	Above is the correlation heatmap for all the continuous variables in the dataset.

•	The variables ‘systolic BP’ and ‘diastolic BP’ are highly correlated.




## **Feature Engineering:**

•	Before performing feature engineering, we have split the data into train- test split to avoid data leakages.

•	 Since, 'sex' and 'is_smoking' columns are in string format. We have encoded them to numerical data type as Encoded (M, F) in sex column as (1,0) Encoded (Yes,No) in is_smoking Column as (1,0).

•	We had null values education,cigsPerDay, BPmeds, total_chol,bmi,glucose, heat rate. We used Simple imputer to impute the null values (median for numerical features and mode of categorical features)

•	In feature selection we used chi square test to select categorical features, since 'sysBP' and 'diaBP' have high correlation, we will drop one of them

•	For Reducing skewness, we used log transformation and square root transformation.

•	Since our dependent variable is unbalanced, we used oversampling technique SMOTE- NC ((Synthetic Minority Oversampling Technique) on training data set. This ensures that the model has trained equally on all kinds of results, and it is not biased to one particular result.

•	Since the predictions from the distance-based models will get affected if the attributes are in different ranges, we need to scale them. We can use StandardScaler to scale down the variables. The results obtained from scaling can be stored and used while building those models. Tree algorithms do not necessarily require scaling



## **Modelling Summary:**

**Logistic Regression**:
* In statistics, the (binary) logistic model is a statistical model that models the probability of one event (out of two alternatives) taking place by having the log-odds (the logarithm of the odds) for the event be a linear combination of one or more independent variables.
  This can be considered as the baseline model to obtain predictions since it is easy to explain.
* Logistic Regression train recall: 0.679
* Logistic Regression test recall: 0.567

**Logistic Regression (With Hyperparameter tuning):**
* Logistic Regression train recall: 0.688
* Logistic Regression test recall: 0.596

**Decision Tree:**
* A Decision tree is a flowchart-like tree structure, where each internal node denotes a test on an attribute, each branch represents an outcome of the test, and each leaf node (terminal node) holds a class label.
* Decision tree train recall: 1
* Decision tree test recall: 0.35

**Decision Tree (With Hyperparameter tuning):**
* Best hyperparameters: 'max_depth': 1, 'min_samples_leaf': 0.1, 'min_samples_split': 0.1
* Decision tree train recall: 0.806
* Decision tree test recall: 0.807

**Random Forests:**
* Random Forest is an ensemble technique capable of performing both regression and classification tasks with the use of multiple decision trees and a technique called Bootstrap and Aggregation, commonly known as bagging. The basic idea behind this is to combine multiple decision trees in determining the final output rather than relying on individual decision trees.
* Random forests train recall: 0.1
* Random forests test recall: 0.317

**Random Forests (With Hyperparameter tuning):**
* Best hyperparameters: max_depth: 2, min_samples_leaf: 0.1, min_samples_split: 0.1, n_estimators: 500
* Random forests train recall: 0.70
* Random forests test recall: 0.66

**XG Boost:**
* In this algorithm, decision trees are created in sequential form. Weights play an important role in XGBoost. Weights are assigned to all the independent variables which are then fed into the decision tree which predicts results. The weight of variables predicted wrong by the tree is increased and these variables are then fed to the second decision tree. These individual classifiers/predictors then ensemble to give a strong and more precise model. It can work on regression, classification, ranking, and user-defined prediction problems.
* XG boost train recall: 0.854
* XG boost test recall: 0.0.365

**Support Vector Machine:**
* Support Vector Machine (SVM) is a supervised machine learning algorithm used for both classification and regression. The objective of SVM algorithm is to find a hyperplane in an N-dimensional space that distinctly classifies the data points.
* SVM train recall: 0.701
* SVM test recall: 0.673

**K-nearest Neighbors:**
* The k-nearest neighbors algorithm, also known as KNN, is a non-parametric, supervised learning classifier, which uses proximity to make classifications or predictions about the grouping of an individual data point.
* K nearest neighbors train recall: 0.924
* K nearest neighbors test recall: 0.461




## **Results:**

|S.no|Model|Train Recall| Test Recall|
|----|-----|------------|------------|
|1   |  Logistic Regression|0.679|0.567
2	|Logistic Regression (With Hyperparameter Tuning)|	0.688	|0.596
3	|Decision Tree|	1	|0.355
4	|Decision Tree (With Hyperparameter Tuning)	|0.806	|0.807
5	|Random Forest|	1	|0.317
6	|Random Forest (With Hyperparameter Tuning)|	0.693	|0.605
7	|GB Boost	|0.854	|0.365
8	|SVM	|0.701	|0.673
9	|KNN	|0.924	|0.461



## **Conclusions:**
* Predicting the risk of coronary heart disease is critical for reducing fatalities caused by this illness. We can avert deaths by taking the required medications and precautions if we can foresee the danger of this sickness ahead of time.
* It is critical that the model we develop has a high recall score. It is OK if the model incorrectly identifies a healthy patient as a high risk patient because it will not result in death, but if a high risk patient is incorrectly labelled as healthy, it may result in fatality.
* We were able to create a model with a recall of just 0.807 because of lack of data and limitations in computational power availability.
* Recall of 0.807 indicates that out of 100 individuals with the illness, our model will be able to classify only 80 as high risk patients, while the remaining 22 will be misclassified.
* Future developments must include a strategy to improve the model recall score, enabling us to save even more lives from this disease.
* This may include more such studies, and collect more data. Include more people with hypertension, diabetes, BP medication, etc to better understand the effect of these disease on the risk of CHD. Also, with better computational abilities, it will be possible to get the best hyperparameters that yield the best predictions.


## References: 
* GeekforGeeks
* Towards data science
* Analytics Vidhya
* ProjectPro
* Kaggle
* W3 school
* Pythonguides
* Stackoverflow
* Python libraries technical documentation
* Krish Naik on Youtube
* Codebasics on Youtube
* 3blue1brown on Youtube
