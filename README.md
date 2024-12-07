# Anaylsis of Cardiovascular Disease Biomarker Homocysteine among Non-Smokers

Author: Amber Campbell

## Introduction
### General Introduction
Cardiovascular disease has been the leading cause of death for both men and women in the United States since 1950. There are many known risk factors for cardiovascular disease including high blood pressure, high cholesterol, and smoking. Homocysteine, a naturally-occuring amino acid in the body, is often used as a biomarker for cardiovascular disease. While homocysteine is broken down by folate, Vitamin B12, and Vitamin B6 to generate chemicals the body needs, high levels of homocysteine can damange artery linings in the body and blood clots, significantly increasing the risk of cardiovascular disease. Research has long supported the notion of homocysteine as a biomarker for cardiovascular disease, and recent advocates support the use of its monitoring and measurement as a guide for disease prevention. 

The dataset I am using comes from the National Health and Nutrition Examination Survey (NHANES) 2005-2006 cohort study, in which demographic,socioeconomic, dietary, and health-related questions are collected from a nationally representative sample. Because smoking is such a well-identified risk factor for cardiovascular disease, the qustion I am intending to focus on is how demographic and health factors relate to a person's homocysteine levels, including diet quality, BMI, sex, race, blood pressure, and total cholesterol. Using such information, I created several prediction models to to predict a person's homocysteine level vased on these metrics. Such a prediction model can be used as an investigative tool for the risks of cardiovascular disease, with homocysteine serving as a proxy measure of an individual's risk for cardiovascular disease. 


### Introduction of Columns
 This dataset was prefiltered in attempts to only include non-smokers by excluding any persons who had smoked over 100 cigarettes in their lifetime or had smoked within 5 days of taking the survey. There are 2033 rows in this dataset, representing health and demographic information for 2033 participants of the NHANES survey. The dataset contains the following relevant columns: 
| Column                                        | Description |
| --------                                      | ------- |
| <code>id</code> (SEQN)                        | Participants sequence number in NHANES study   |
| <code>homocysteine</code> (LBXHCY)            | Homocysteine measurement (umol/L)   |
| <code>cotinine</code> (LBXCOT)                | Cotinin measurement-biomarker for tobacco smoke exposure (ng/mL)    |
| <code>sex</code> (RIAGENDR)                   | Sex (Male, Female)    |
| <code>age</code> (RIDAGEYR)                   | Age (years)    |
| <code>race</code> (RIDRETH1)                  | Race    |
| <code>education_level</code> (DMDEDUC2)       | Higest Education Achieved    |
| <code>bmi</code> (BMXBMI)                     | BMI    |
| <code>diet_level</code> (DBQ700)              | Diet Quality    |
| <code>WkAlcDays</code>                        | Average number of alcoholic drinks per week |
| <code>diabetes_status</code> (DIQ010)         | Diabetes Status (Borderline, Yes, No)  |
| <code>systolic_bp</code> (BPXSY1)             | Systolic Blood Pressure (mmHg)    |
| <code>cholesterol</code> (LBXTC)              | Total Cholesterol (mg/dL)   |


## Data Cleaning and Exploratory Analysis
### Data Cleaning
### Univariate Analysis
### Bivariate Analysis
### Interesting Aggregates
### Missing Value Imputation

## Framing a Prediction Problem
### Problem Identification

## Baseline Model
## Final Model