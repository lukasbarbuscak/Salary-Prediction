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

![salary_outliers](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/salary_outliers.PNG)

Even though the data had some visible outliers when it came it salary, a closer look at the data showed no errors. These jobs paid better because of being senior positions in high-pay industries. The data also contained some duplicate values, and I simply dropped them. The final shape of the dataset is 999,809 rows and 8 columns.

## Exploratory Data Analysis
Before building models, I looked at the data using EDA and tried to make predictions about the relationships between the variables. First, I checked if there are any differences between groups of data. When it comes to mean differences between the groups and distances/years of experience, there were either very small, or none at all.

There seemed to be no mean differences in salary between postings of different companies, and small differences between majors required for the positions (the only difference was having a major or not having a major). However, when it comes to job type, industry, and degree, the mean differences were bigger, and appeared to be significant in general, so I created boxplots for those categorical variables:

![salary_by_jobtype](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/salary_by_jobtype.PNG)

![salary_by_industry](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/salary_by_industry.PNG)

![salary_by_degree](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/salary_by_degree.PNG)

Generally, not surprisingly, CEO positions have the highest salary, and janitor positions have the lowest salary. There are differences between industries, with oil and finance being the with the highest mean, and service and education the lowest. Also, in general, more education (represented by the degree obtained) means better pay.

I also checked the distributions of each categorical variable, and found that this dataset seemed extremely balanced in terms of distribution of each categorical variable. The job type count was roughly the same for all job types, there was only slightly more people with no major/without post-secondary education in the dataset than their counterparts, and all industries and companies were represented roughly equally. As an example:


![countplot](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/countplot.PNG)

After exploring the categorical variables and their relationships to the salary variable, I took a closer look at numerical variables. Firstly, I was curious about the distribution of the numerical variables.

