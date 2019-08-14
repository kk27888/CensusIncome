Census Income Data Set Analysis
===============================

Introduction:
------------

Many data mining tasks require classification of data into classes. For example, loan applications can be classified into either approve or disapprove classes. A classifier provides a function that maps (classifies) a data item (instance) into one of several predefined classes. The automatic induction of classifiers from data not only provides a classifier that can be used to map new instances into their classes but may also provide a human-comprehensible characterization of the classes. In many cases, interpretability-the ability to understand the output of the induction algorithm-is a crucial step in the design and analysis cycle. Some classifiers are naturally easier to interpret than others; for example, decision-trees are easy to visualize, while neural – networks are much harder. <br>

This data was extracted from the census bureau database found at http://www.census.gov/ftp/pub /DES/www/welcome.html . The Census Bureau is dedicated to providing current facts and figures about America’s people, places, and economy. It provides the best mix of timeliness, relevancy, quality and cost for the data collected and services provided. Extraction was done by Barry Becker from the 1994 Census database. A set of reasonably clean records was extracted using the following conditions: ((AAGE>16) && (AGI>100) && (AFNLWGT>1) && (HRSWK>0)).


Dataset Description:
-------------------

Below is a list of attributes in the dataset with their type and description. The census data has a number of variables like age, workclass, education, marital-status, occupation, race, etc. that will help in determining the income of an individual.  
•	Listing of attributes: >50K, <=50K.
•	age: continuous.
•	workclass: Private, Self-emp-not-inc, Self-emp-inc, Federal-gov, Local-gov, State-gov, Without-pay, Never-worked.
•	fnlwgt: continuous.
•	education: Bachelors, Some-college, 11th, HS-grad, Prof-school, Assoc-acdm, Assoc-voc, 9th, 7th-8th, 12th, Masters, 1st-4th, 10th, Doctorate, 5th-6th, Preschool.
•	education-num: continuous.
•	marital-status: Married-civ-spouse, Divorced, Never-married, Separated, Widowed, Married-spouse-absent, Married-AF-spouse.
•	occupation: Tech-support, Craft-repair, Other-service, Sales, Exec-managerial, Prof-specialty, Handlers-cleaners, Machine-op-inspct, Adm-clerical, Farming-fishing, Transport-moving, Priv-house-serv, Protective-serv, Armed-Forces.
•	relationship: Wife, Own-child, Husband, Not-in-family, Other-relative, Unmarried.
•	race: White, Asian-Pac-Islander, Amer-Indian-Eskimo, Other, Black.
•	sex: Female, Male.
•	capital-gain: continuous.
•	capital-loss: continuous.
•	hours-per-week: continuous.
•	native-country: United-States, Cambodia, England, Puerto-Rico, Canada, Germany, Outlying-US(Guam-USVI-etc), India, Japan, Greece, South, China, Cuba, Iran, Honduras, Philippines, Italy, Poland, Jamaica, Vietnam, Mexico, Portugal, Ireland, France, Dominican-Republic, Laos, Ecuador, Taiwan, Haiti, Columbia, Hungary, Guatemala, Nicaragua, Scotland, Thailand, Yugoslavia, El-Salvador, Trinadad&Tobago, Peru, Hong, Holand-Netherlands.

Analysis objectives:
--------------------

1.	What are the most important features that make influences on income?
2.	To create a forecast model to make classification of people whose income <= 50k and >50k annually.


Data Preprocessing:
-------------------

1.	Data Cleaning: 
Firstly, I checked all the unknown or not available values in data set. Basically, there are only 3 columns who have values like “?” which need to be cleaned. After spotting those values and delete all the observations, my dataset still has 30162 observations and 15 variables.
2.	Creating Dummy Variables:
One big problem for classification is to take care of those categorical data. Many variables like workclass, sex and education, the datatype of those values is string. So I created some dummy variables for those string value to transform them into numeric. After creating dummy variables, my data set has 30162 observations and 89 columns.
3.	Splitting the Dataset 
After creating dummy variables, I split the whole dataset for further analysis. 60% of dataset is for training, 30% is for validation and 10% is for testing. I use training dataset to train the different models and use validation dataset to show how well these models fit. And finally, I’ll use testing dataset to see the performance of my best model.
4.	Feature Selection
Because the dataset is very large and it takes very long time for me to apply some machine learning models to fit this dataset, we decide to list the most important and significant features and only use the first 20. The method we use is “importance “ function in sklearn.random_forest. The first 20 most important features are listed below:
 
1. Married-civ-spouse 
2. capital-gain
3. education-num 
4. Husband
5. age 
6. Never-married 
7. hours-per-week 
8. capital-loss
9. Exec-managerial 
10. Prof-specialty
11. Exec-managerial 
12. Prof-specialty
13. fnlwgt 
14. Female
15. Wife
16. Not-in-family 
17. Own-child
18. Male 
19. Divorced
20. Other-service
As you can see, many of them are dummy variables like “Married-civ-spouse”. We also have some numeric variable like “age”.

Analysis Experiments:
---------------------

We chose Random Forest, SVM and Naïve Bayes as our analysis models because these three are all supervised machine learning models. Since our data is with label, supervised machine learning models are supposed to have better forecast performance than unsupervised models.

1.	Random Forest Classification
The first model that we tried is random forest. We trained the model by training data and used validation data to measure the accuracy. After fine-tuning the parameters, we found when estimators = 200 and max_depth = 11, it performs best. In this case, the accuracy of this model is 86%. To look into the results, we created the confusion matrix for result interpretation. The true-positive rate and false-positive rate are very high. The only drawback of this model is false-negative rate is a little bit high also. Overall, this model has a very good performance.
 
2.	Support Vector Machine Classification
The second model that we tried is Support vector Machine. This model ran very slowly and took us a lot of time because of our large dataset. After fine-tuning the parameters, we found when kernel is linear and c (Penalty parameter C of the error term) is 1.0, it performs best. In this case, the accuracy of this model is 79%. Below is the confusion matrix of SVM classification. The main difference of svm and random forest is false-negative rate and false-positive rate. To make it clear, a lot of people whose income is greater than 50k but svm classify them into the wrong category.
 
3.	Naïve Bayes Classification
The final model that we tried is naïve bayes classification.  After fine-tuning the parameters, we found when alpha (Additive (Laplace/Lidstone) smoothing parameter) is 1.0, it performs best. In this case, the accuracy of this model is 77%.  From this confusion matrix, we can see it has the same problem with svm: too much false negative.
 

Conclusion:
-----------
1.	After comparison of different models, we found our best model is random forest classification with estimator = 200 and max depth = 11. So, we apply this model in testing dataset and its accuracy is 84.91%, still high respectively.

2.	Since we’ve already known the most significant features, my next step is to focus on how these features affect income, positively or negatively.




