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
![alt tag](https://github.com/lukasbarbuscak/Salary-Prediction/blob/master/images/salary_outliers.PNG)
