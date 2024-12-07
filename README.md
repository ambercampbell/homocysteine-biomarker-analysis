# Analysis of Homocysteine as a Biomarker for Cardiovascular Disease Among Non-Smokers
By Amber Campbell
## Introduction
### General Introduction
Cardiovascular disease has been the leading cause of death for both men and women in the United States since 1950. There are many known risk factors for cardiovascular disease including high blood pressure, high cholesterol, and smoking. Homocysteine, a naturally-occuring amino acid in the body, is often used as a biomarker for cardiovascular disease. While homocysteine is broken down by folate, Vitamin B12, and Vitamin B6 to generate chemicals the body needs, high levels of homocysteine can damange artery linings in the body and blood clots, significantly increasing the risk of cardiovascular disease. Research has long supported the notion of homocysteine as a biomarker for cardiovascular disease, and recent advocates support the use of its monitoring and measurement as a guide for disease prevention(). 

The dataset I am using comes from the National Health and Nutrition Examination Survey (NHANES) 2005-2006 cohort study, in which demographic,socioeconomic, dietary, and health-related questions are collected from a nationally representative sample. Because smoking is such a well-identified risk factor for cardiovascular disease, the qustion I am intending to focus on is how demographic and health factors relate to a person's homocysteine levels, including diet quality, BMI, sex, race, blood pressure, and total cholesterol. Using such information, I created several prediction models to to predict a person's homocysteine level vased on these metrics. Such a prediction model can be used as an investigative tool for the risks of cardiovascular disease, with homocysteine serving as a proxy measure of an individual's risk for cardiovascular disease. 


### Introduction of Columns
 This dataset was prefiltered in attempts to only include non-smokers by excluding any persons who had smoked over 100 cigarettes in their lifetime or had smoked within 5 days of taking the survey. There are 2033 rows in this dataset, representing health and demographic information for 2033 participants of the NHANES survey. The dataset contains the following relevant columns: 


| Column                      | Description                                                         |
|-----------------------------|---------------------------------------------------------------------|
| `id` (SEQN)                 | Participants sequence number in NHANES study                        |
| `homocysteine` (LBXHCY)     | Homocysteine measurement (umol/L)                                   |
| `cotinine` (LBXCOT)         | Cotinine measurement - biomarker for tobacco smoke exposure (ng/mL) |
| `sex` (RIAGENDR)            | Sex (Male, Female)                                                  |
| `age` (RIDAGEYR)            | Age (years)                                                         |
| `race` (RIDRETH1)           | Race                                                                |
| `education_level` (DMDEDUC2)| Highest Education Achieved (No/Some/All High School, Some/All College)      |
| `bmi` (BMXBMI)              | BMI (kg/b^2^)                                                       |
| `diet_level` (DBQ700)       | Self-desribed Diet Quality (Poor, Fair, Good, Very Good, Excellent) |
| `WkAlcDays`                 | Average number of alcoholic drinks per week                         |
| `diabetes_status` (DIQ010)  | Diabetes Status (Borderline, Yes, No)                               |
| `systolic_bp` (BPXSY1)      | Systolic Blood Pressure (mmHg)                                      |
| `cholesterol` (LBXTC)       | Total Cholesterol (mg/dL)                                           |



## Data Cleaning and Exploratory Analysis
### Data Cleaning
 1. I started by renaming the columns (indicated in parentheses in the previous table) to be more easily-comprehendable. 
 2. I then verified that each row in the dataset had a unique ID, and thus no duplicate information about each participant from the study. I then checked relevant columns `homocysteine`, `age`, `bmi`, `systolic_bp`, and `cholesterol` for values of 0, which are likely indicators of missing values, because they are all measurements that should have values above 0. While none of these columns had values of 0, I noticed some extreme values for BMI (such as 130). While acknowledging that BMI is a controversial and more recently viewed as a misused or inaccurate measurement, it is highly unlikely for BMI values to be above 50, and I those chose to remove any rows from the dataset that contained BMI measurements over 54 after looking into this more ([CDC](https://www.nhlbi.nih.gov/health/educational/lose_wt/BMI/bmi_tbl.pdf), [Cleveland Clinic](https://my.clevelandclinic.org/health/diseases/21989-class-iii-obesity-formerly-known-as-morbid-obesity)). 
 3. I then inspected the categorial columns, making sure that the unique values in each column were comprehendable. The `diabetes_status` column had a range of values including 'Yes', 'No', 'Borderline', and 'Borderlinederline'. I corrected any instances of 'Borderlinederline' to match 'Borderline'.

My resulting dataframe contained 1099 rows. 
The first few rows of this cleaned dataset are shown below. 

|    id |   homocysteine |   cotinine | sex    |   age | race          | education_level   |   bmi | diet_level   | diabetes_status   |   systolic_bp |   cholesterol |   WkAlcDays |
|------:|---------------:|-----------:|:-------|------:|:--------------|:------------------|------:|:-------------|:------------------|--------------:|--------------:|------------:|
| 31131 |           9.33 |      0.035 | Female |    44 | Black         | SomeCollege       | 30.9  | Good         | No                |           144 |           105 |           0 |
| 31132 |           8.96 |      0.021 | Male   |    70 | White         | College           | 24.74 | VeryGood     | Yes               |           138 |           147 |           4 |
| 31134 |           8.2  |      0.065 | Male   |    73 | White         | HighSchool        | 30.63 | Good         | No                |           130 |           186 |           2 |
| 31144 |           7.97 |      0.125 | Male   |    21 | OtherHispanic | HighSchool        | 25.03 | Excellent    | No                |           116 |           207 |           0 |
| 31149 |          10.29 |      0.011 | Female |    85 | White         | SomeHighSchool    | 21.63 | Good         | No                |           110 |           121 |         nan |

### Univariate Analysis
I first examined by main measurements of interest, homocysteine. 
<iframe
  src="assets/homocysteine-dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Describe Distribution

### Bivariate Analysis
<iframe
  src="assets/homocysteine-race.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### Interesting Aggregates

Pivot table using diabetes status

| diabetes_status   |     bmi |   cholesterol |   cotinine |   homocysteine |   systolic_bp |
|:------------------|--------:|--------------:|-----------:|---------------:|--------------:|
| Borderline        | 33.4398 |       200.412 |   0.262382 |        8.30324 |       133.549 |
| No                | 28.6295 |       201.569 |   0.162658 |        7.64186 |       122.485 |
| Yes               | 31.8165 |       192.099 |   0.120988 |        9.17927 |       132.996 |


### Missing Value Imputation

Imputed Using mean for numerical columns and most common value for categorical columns.

There were 21 missing BMI measurements
<iframe
  src="assets/bmi-imputation.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

There were 220 missing systolic blood pressure measurements
<iframe
  src="assets/bp-imputation.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

There were 13 missing total cholesterol measurements
<iframe
  src="assets/cholesterol-imputation.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

There were 11 missing cotinine measurements
<iframe
  src="assets/cholesterol-imputation.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

There were 2 missing diabetes status values
<iframe
  src="assets/diabetes-imputation.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

  There were 4 missing diet quality values
<iframe
  src="assets/diet-imputation.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



## Framing a Prediction Problem
From the univariate and bivariate analyses, I noticed that homocysteine levels tended to vary for participants of different races and diabetes statuses. Thus, my prediction problem will be ==predicting a person's homocysteine levels using such demographic and health information==. This is a ==regression problem==, with ==homocysteine as the prediction variable==. I chose ==MSE== as my evaluation metric because it tends to provides an easily understandable ,measure of how similar the prediction levels are to the actual homocysteine levels, and it penalizes larger errors more heavily than smaller errors. All of the information presented in the dataset would be known at time of prediction, because they are all health measurements or demographic identifications that are independent of one another. 
## Baseline Model
## Final Model