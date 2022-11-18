# EDA-default-risk-analysis

# INTRODUCTION

This case study aims to give an idea of applying EDA in a real business scenario. In this case study, we will apply the EDA techniques towards developing a basic understanding of risk analytics in banking and financial services and understand how data is used to minimise the risk of losing money while lending to customers.

This case study aims to identify patterns which indicate if a client has difficulty paying their instalments which may be used for taking actions such as denying the loan, reducing the amount of loan, lending (to risky applicants) at a higher interest rate, etc. 

This will ensure that the consumers capable of repaying the loan are not rejected. Identification of such applicants using EDA is the aim of this case study.

# CURRENT LOAN APPLICATION DATA

## Inspection & Cleaning

After reading and inspecting the dataset, we performed missing data analysis and the below points can be considered towards missing data imputation:
- Columns with more than 50% missing data can be dropped 
- Columns with 13% or lower missing values, can be imputed with mode, median or mean depending on the type of the column and data distribution
- Categorical columns with > 20% but < 50% missing data can have a new type such as ‘Unknown’ for missing data imputation.

##### Data type correction

- The columns representing the number of enquires to Credit Bureau about the client are of float data type. We can change the data type to int.
- DAYS  related columns and CNT_FAM_MEMBERS can be changed to int data type as they represent number of days  and family member count respectively.

##### Data Standardization

- DAYS  related columns have some negative values. They can be replaced with their respective absolute values.
- We can create a new column based on DAYS_BIRTH to show the age of the applicant for better readability and then we can drop the DAYS_BIRTH column. Similarly we can convert the other DAYS columns to represent the value in years.
- The CODE_GENDER column has XNA values that can be replaced with nan.

##### Outlier Analysis

- AMT_INCOME_TOTAL has very high valued outliers. As we know the income may vary from person to person, we can cap value here and get rid of very high incomes.

![image](https://user-images.githubusercontent.com/103338455/162632598-5fd730c4-50bb-4444-b38a-27fa8d177444.png)

- DAYS_EMPLOYED has huge outliers. Some data points are showing close to 1000 years in service which is impossible. We can cap the value at a desired point after analysing the quantiles.

![image](https://user-images.githubusercontent.com/103338455/162632646-9d0939a5-99db-4f66-bbb9-d2dae0f46480.png)

##### Binning

We may want to bin the applicants ages into certain categories to be able to draw some insights such as - whether the loan defaulters majorly fall into any certain age groups or which age groups are much likely to repay on time etc.

![image](https://user-images.githubusercontent.com/103338455/162632719-5ad1e26f-2505-476b-831b-847a7e22b523.png)

![image](https://user-images.githubusercontent.com/103338455/162632723-513a5dfc-2440-4fce-a50a-3a58158713c3.png)

##### Imbalance Percentage

![image](https://user-images.githubusercontent.com/103338455/162632738-5b9dc31a-552a-4166-9a72-04fde05cae29.png)

- The 'TARGET‘ column represents whether the client is a defaulter or not.  If we segregate our dataset based on this column, and if the distribution turns out to be 50-50, then our data set would be BALANCED.  In any other case, it would be considered as IMBALANCED. 
- As per the plot, we can say that our data set is imbalanced with almost 8% defaulters. Rest all 92% were able to repay the loans.
- We then created 2 data sets to segregate  our original data based on the TARGET column values to have defaulters in one dataframe and others in another.


## Univariate Analysis

##### Categorical

![image](https://user-images.githubusercontent.com/103338455/162632833-a66b1c98-3891-4fea-b2a7-28b32b1dcb24.png)

Cash loan type contracts have higher defaulters.

##### Numerical

![image](https://user-images.githubusercontent.com/103338455/162632859-8835176e-622c-4068-a26f-fb87838b6e9a.png)

- Defaulters are more in 25-40 age group. 
- Above 40, the number of defaulters tends to decrease.

![image](https://user-images.githubusercontent.com/103338455/162632880-27c4e1ec-ddbb-4bc8-999c-7eae223d577f.png)

Most of the defaulters are in low income range.

##### Correlation

![image](https://user-images.githubusercontent.com/103338455/162632905-e9b1745b-da67-40ce-b585-696548fb9c60.png)

AMT_CREDIT is strongly correlated to AMT_ANNUITY and AMT_GOODS_PRICE in both cases.


## Bivariate Analysis

##### Categorical  - Categorical  

![image](https://user-images.githubusercontent.com/103338455/162632951-15da57f3-3fbb-46c0-bb12-1c635b0f5923.png)

- Single and civil marriage applicants are more likely to default.
- People staying in rented apartment or with parents might default.

![image](https://user-images.githubusercontent.com/103338455/162632978-b76cdad7-a329-4830-83e5-6e13a15332ac.png)

- Across income types, cash loan seems to be the popular contract type.
- Most of the people who have taken loans are working class and they have taken cash loans mostly compared to revolving loans.
- People who have taken cash loans are likely to default as well.

##### Categorical  - Continuous

![image](https://user-images.githubusercontent.com/103338455/162633013-8b00acea-ba54-4073-98c5-e6f127e75087.png)

- Loan amount taken by businessman is higher compared to the other income types.
- People with maternity leave income type tend to default with higher credit amount.

![image](https://user-images.githubusercontent.com/103338455/162633030-30c844ad-5945-4645-abcd-7c2b858fd2af.png)

- People having academic degree and higher education have more loan annuity amount compared to the other groups.
- People with lower secondary education level are more likely to fail repayment. 
- People with academic degree or higher education, have no difficulty in repayment.

##### Continuous  - Continuous

![image](https://user-images.githubusercontent.com/103338455/162633064-3c2afe0e-395b-4f95-8f5b-a734d66acc96.png)

![image](https://user-images.githubusercontent.com/103338455/162633070-d52b201a-d0aa-446c-b32d-3b7f1fe15733.png)

- With an increase in credit amount, annuity and goods price, the tendency to default decreases. 
- High chances of defaulting for lower credit amount, annuity and goods price.


# PREVIOUS LOAN APPLICATION DATA

## Inspection & Cleaning

- After reading and inspecting the dataset, we performed missing data analysis .
- The columns with more than 50% missing data can be dropped 

## Data Standardization

The DAYS columns seem to have some negative values. We must convert that to absolute value.

## Outlier Analysis

![image](https://user-images.githubusercontent.com/103338455/162633165-06eb8810-b433-42b1-8e22-4e4f3b478748.png)

Annuity seems to have some higher data points. The outliers can be capped at 0.99.

![image](https://user-images.githubusercontent.com/103338455/162633177-0b2c9470-894e-4da3-b811-621e7f8a867b.png)

There are certain highly priced goods after 0.95 quantile. Here we can set a cap value to ignore very high goods price.


# MERGING DATA SETS

Merge the application data frame and previous application data frame based on the column  SK_ID_CURR. Post merging the duplicate columns those are required for our analysis can be renamed. We can drop the unwanted columns from the merged data frame.

## Imbalance Percentage

![image](https://user-images.githubusercontent.com/103338455/162633213-12e52bbc-4137-40c7-8025-4cd3775f4ff5.png)

The previous data also seems imbalanced.

## Univariate Analysis

##### Categorical

![image](https://user-images.githubusercontent.com/103338455/162633255-22440a43-dcb0-4297-aa5c-b9d747782e0e.png)

- High number of defaults in case of cash loans followed by consumer loans in previous applications data.
- There are some missing contract types in the data.

![image](https://user-images.githubusercontent.com/103338455/162633268-cea3d4fb-b62d-47c5-a34e-5b3aedd8a617.png)

- High number of defaulters have their loans approved in the past.
- Number of defaulters who have not used the offer is the minimum.

##### Numerical

![image](https://user-images.githubusercontent.com/103338455/162633286-fe1cb194-b03c-4b53-b44d-3c74a5254dc5.png)

In past, most of the loans had credit amount in the lower range i.e. below 1 lakh.

![image](https://user-images.githubusercontent.com/103338455/162633299-a9e038a5-7d44-4ceb-978a-7a96ba552de7.png)

Previous applications annuity was also mostly below 1 lakh.

##### Correlation

![image](https://user-images.githubusercontent.com/103338455/162633319-b4d2db38-f7e6-4695-a409-e60fbd7b6c4c.png)

AMT_CREDIT_PREV is highly correlated to AMT_APPLICATION and AMT_GOODS_PRICE_PREV.

## Bivariate Analysis

##### Categorical - Categorical  

![image](https://user-images.githubusercontent.com/103338455/162633374-d8bc2b1d-be42-435c-b011-7d89d1f1fe06.png)

Number of loans taken for Repairs purpose is higher compared to others. Hence, the number of defaulters might be high in this group.

![image](https://user-images.githubusercontent.com/103338455/162633391-32061b8b-d603-44ba-996f-7a39e51aa9a2.png)

- Most of the applications were rejected for rejection code - HC. It also has the higher number of defaulters.
- Rejection by system is very less.

##### Categorical - Continuous

![image](https://user-images.githubusercontent.com/103338455/162633437-5ce47bad-6447-451f-a9af-025359bb34fd.png)

People taking cash loans but have refused to name the purpose are more likely to default and people who have applied loan for buying a home are more likely to repay on time.

![image](https://user-images.githubusercontent.com/103338455/162633452-8b1102b0-a8f6-4b6f-8e35-ad54153b2598.png)

People who have unused offers are more likely to default even though they have comparatively high total income

##### Continuous  - Continuous

![image](https://user-images.githubusercontent.com/103338455/162633477-270868ff-e448-4b39-bec0-8a67309d4445.png)

![image](https://user-images.githubusercontent.com/103338455/162633482-95305fdc-c0f1-4fc5-9330-97d014aa2b82.png)

- With an increase in credit amount, applied amount and goods price, the tendency to default decreases.
- High chances of defaulting for lower credit amount, applied amount and goods price.

# INFERENCES

## People who are more likely to default

- Age : Young people – 25 to 35 age group
- Income : Lower income group with a total income of less than 5 lakhs
- Occupation : Low-skill labourers, drivers, waiters/barmen staff
- Education : Lower / secondary education
- Gender : Males
- Income type : On maternity leave and unemployed
- Family status : Civil marriage, single/unmarried
- Housing type : Rented apartment or with parents
- Contract type: Cash loan 
- Cash loan purpose : Repairs and urgent needs
- Previous loan status : Approved 

## People who will repay on time

- Age : Older people – above 50
- Income : Higher income group 
- Occupation : Managers, High-skilled tech staff, Accountants
- Education : Higher education and academic degree
- Gender : Females
- Income type : Working class, businessmen and students
- Family status : Married
- Housing type : Own house/apartment
- Contract type: Revolving loan 
- Cash loan purpose : Buying garage, home etc.
- Previous loan status : Unused offer


# CONCLUSION

- Young males with lower secondary education and of lower income group and staying with parents or in a rented house, applying for low-range cash contract, should be denied.
- Females are likely to repay but not if they are on maternity leave. Hence, bank can reduce the loan amount for female applicants who are on maternity leave.
- Since people taking cash loans for repairs and urgent needs are more likely to default, bank can refuse them.
- Since the people who have unused offers are more likely to default even though they have comparatively high total income, they can be offered loan at a higher interest rate.
- Banks can target businessmen, students and working class people with academic degree/ higher education as they have no difficulty in repayment.
- Bank can also approve loans taken on purpose for buying home or garage as there less chances of defaulting. 
