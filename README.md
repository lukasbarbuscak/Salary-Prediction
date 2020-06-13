# Predicting Salaries of Future Job Postings

## Introduction
How are salaries for specific job positions determined? Is it simply based on experience and type of position of potential job applicants, or is there more to it? I would like to investigate this question using data on present job postings, and their attached salaries. After exploring the data, I will develop a model and plot which features are the most important in determining salaries of newly posted posittions. The language of choice to tackle this problem is Python, using packages such as pandas, numpy, matplotlib, seaborn, and sklearn.

## Data Cleaning
My data contains one million observations, and variables included are:
- company ID number: each posting has information on which company has posted the vacancy
- job type: based on seniority, such as CEO, CFO, or junior
- degree: college degree required for a job
- major: university major included in job description
- industry: general industry of the company
- experience: number of years of experience required for the given job and job type
- distance: number of miles from major city
- salary: posted salary in a job posting

Although the data I got was relatively clean, I had to delete 5 observations which had salary listed as 0, and check for potential outliers. The boxplot of the salary variable looks like this:

<br /> 

![salary_outliers](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/salary_outliers.PNG)

Even though the data had some visible outliers when it came it salary, a closer look at the data showed no errors. These jobs paid better because of being senior positions in high-pay industries. The data also contained some duplicate values, and I simply dropped them. The final shape of the dataset is 999,809 rows and 8 columns.

## Exploratory Data Analysis
Before building models, I looked at the data using EDA and tried to make predictions about the relationships between the variables. First, I checked if there are any differences between groups of data. When it comes to mean differences between the groups and distances/years of experience, there were either very small, or none at all.

There seemed to be no mean differences in salary between postings of different companies, and small differences between majors required for the positions (the only difference was having a major or not having a major). However, when it comes to job type, industry, and degree, the mean differences were bigger, and appeared to be significant in general, so I created boxplots for those categorical variables:

<br /> 

![salary_by_jobtype](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/salary_by_jobtype.PNG)

![salary_by_industry](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/salary_by_industry.PNG)

![salary_by_degree](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/salary_by_degree.PNG)

Generally, not surprisingly, CEO positions have the highest salary, and janitor positions have the lowest salary. There are differences between industries, with oil and finance being the with the highest mean, and service and education the lowest. Also, in general, more education (represented by the degree obtained) means better pay.

I also checked the distributions of each categorical variable, and found that this dataset seemed extremely balanced in terms of distribution of each categorical variable. The job type count was roughly the same for all job types, there was only slightly more people with no major/without post-secondary education in the dataset than their counterparts, and all industries and companies were represented roughly equally. As an example:

<br /> 

![countplot](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/countplot.PNG)

<br />  After exploring the categorical variables and their relationships to the salary variable, I took a closer look at numerical variables. Firstly, I was curious about the distribution of the numerical variables.

<br /> 

![num_distributions](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/num_distributions.PNG)

<br /> The distance from the major city seems very similar for all the observations, and shows a uniform distribution. The salary graph shows slight skewness to the right, but the shape overall follows normal distribution. The years of experience variable shows again a uniform shape, suggesting once again a balanced dataset.

Lastly, I wanted to explore the nature of the relationship between salary and other numerical variables. Salaries generally decrease with larger distance from the major city, and they tend to increase with years of experience.

<br /> 
<br /> 

![exp_salary](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/exp_salary.PNG) 
![distance_salary](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/distance_salary.PNG)

## Modeling

Because this is a regression problem with the dependent variable being a continuous one, MSE was a simple and fitting choice to use as a metric for my model. As my baseline model, I used a "difference from average salary", since every ML model should be able to outperform differences from the mean. The MSE for my baseline model was 1498.837. 

I chose three models that had a potential to improve this MSE:
- Linear Regression: as seen in the EDA, the data follows a relatively linear shape
- Decision Trees: just like linear regression, it is a basic and fast approach for modeling, and performs well with linear relationships
- Gradient Boosting: because this is a regression problem, gradient boosting offers great way for weak learners to improve their performance, and is often used to minimize the MSE

I have summarized the results in the following table:

| Model  | MSE |
| ------------- | ------------- |
| Baseline  | 1498.837  |
| Linear Regression  | 384.487  |
| Decision Tree  | 701.008  |
| Gradient Boosting  | 356.896  |

Gradient boosting provided the best result. I saved the model with the following parameters: 

```
GradientBoostingRegressor(alpha=0.9, ccp_alpha=0.0, criterion='friedman_mse',
                          init=None, learning_rate=0.1, loss='ls', max_depth=5,
                          max_features=None, max_leaf_nodes=None,
                          min_impurity_decrease=0.0, min_impurity_split=None,
                          min_samples_leaf=1, min_samples_split=2,
                          min_weight_fraction_leaf=0.0, n_estimators=150,
                          n_iter_no_change=None, presort='deprecated',
                          random_state=None, subsample=1.0, tol=0.0001,
                          validation_fraction=0.1, verbose=0, warm_start=False)
```
I then proceeded to scoring the test dataset using the saved model, and I saved the predictions. As the last step, I wanted to know which features were the most important in the model. Job type, experience, distance, and industry played the most important role in the model. Graphically:

<br /> 

![importances](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/importances.PNG)

## Conclusion
To sum up, I have developed a model that is predicting future salaries of job postings based on salaries of current job postings. After performing the exploratory data analysis, I fitted three models and compared their mean squared errors, basically comparing how well the models performed comparing to the baseline model, and also each other. The model performing the best with the train data was the gradient boosting model. I saved the model, scored the test data with it, and saved the results of the prediction in a csv file. I also included the analysis of feature importances, and saved it in a separate file.

Using gradient boosting and a bit of hyperparameter tuning, I was able to show that the strongest predictors for salary associated with job postings is the job type (or seniority), years of experience, distance from a major city, and specific industry the job posting applies to. Future iterations of this analysis may incorporate more features, such as specific job descriptions/duties, various personality traits, or certifications.
