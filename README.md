# Customer-Churn-Prediction

Image here


## Overview

## 📉 Customer Churn Prediction – Telco Case Study
Predicting and preventing customer churn is one of the most valuable strategies a business can implement, especially in saturated markets like telecommunications. Studies show that:

📌 Acquiring a new customer can cost 5 to 7 times more than retaining an existing one

📌 A 5% increase in customer retention can boost profits by 25% to 95% (Harvard Business Review)

This project leverages customer data from Telco, a telecommunications company, to build a machine learning model that predicts whether a customer is likely to churn. Early identification of high-risk customers allows the company to proactively engage them through tailored retention strategies which help to reduce churn, increase customer lifetime value, and improve overall profitability.


## Dataset

The dataset contains comprehensive information on customer demographics, services used, billing behavior, and account status. Key features include:

Demographics: gender, SeniorCitizen, Partner, Dependents

Services: PhoneService, InternetService, OnlineSecurity, StreamingTV, etc.

Account & Billing: Contract, PaymentMethod, MonthlyCharges, TotalCharges

Target: Churn (Yes/No)

Dataset is composed of 7043 rows and 21 columns. 



# Methodology
The project follows these key steps:

1. Data Preprocessing: Cleaning and preparing the data for analysis.
2. Exploratory Data Analysis: Exploring relationship between features and using visualizations techniques to discover insights.
3. Feature Engineering: Selecting and transforming relevant features to enhance model performance. 
4. Model Development: Implementing machine learning algorithms to predict Churn.
5. Model Evaluation: Assessing the model's accuracy and reliability using appropriate metrics.


# 1) Data Preprocesssing:
In the part of the project I loaded the data and checked for duplicate values and null values. Furthermore I explored the data types and discovered that all were numeric with the exception of two. 

df.head() and df.columns are used to explore the feature of the dataset and begin developing questions to explore during EDA. 


# 2) Exploratory Data Analysis:

 ## Exploring the target variables 
 ![image](https://github.com/user-attachments/assets/58bca2c1-89a4-42ee-b362-14f87f9de364)

## Observation
- 26.6% of customers in this data set Churned.

 ## Distribution of Monthly Charges in Dataset

![image](https://github.com/user-attachments/assets/a223df14-e9df-4e11-a120-57e683c11306)



 ## Observations:
 - Most customers are paying between $20-$26 per month.
 - Average amount paid is $64.80 per month.
 - Standard Deviation is ~$30

## Distribution of Monthly Charges by Churn

![image](https://github.com/user-attachments/assets/9a0af3e6-c8a6-46e4-8a31-36c7259f527a)

## Observation
- By far, customers who churned were paying more per month than those who did not.
- Is there a reason for this?

## Average Monthly Charges by Contract Type and Churn Status

![image](https://github.com/user-attachments/assets/11077efb-f7f5-448a-81c7-46c62e8beca8)

## Observations: Churn, Contract Type and Average Monthly Charges
- On average customers who churned were paying more per month than those who did not, this was true regardless of the type of contract.
- Customers who were month-to-month and churned were paying on average $12 more per month than those who did not churn.
- Customers who were on a year conctract and churned were paying on average $23 more than customers on a year contract who did not churn. 
- Customers who churned and on a two year contract were on average paying $26 more than customers who did not churn and were on a two year contract. 

### Churn Distribution by Contract Type
![image](https://github.com/user-attachments/assets/4088c502-9269-4407-9664-5675066a7a5b)

## Observation: Churn and Contract Type
- 27% of Telco customers in data set churned. 
- Of the 1869 customers (27%) who churned, 1655 (24%) of these were on a Month-to-month contract. 
- This is a cleary indicates that customers at risk of churning are on a Month-to-month contract. 
- Of the total customers who churned only 2% were on a year contract.
- Of the customers who churned only 1% were on a Two year contract.  

## Overlay of Monthly Charges by Churn Status

![image](https://github.com/user-attachments/assets/699290f8-397a-4735-a457-ad56d218ebbd)

## Observation
- Based on these visualizations it is clear that customers who are on a month-to-month contract and pay between $20-$30 a month churn at rates far lower to customers who are month-to month and pay $70-$100.
- This is great insight since it can help Telco focus intervention methods on customers who are month-to-month paying between $70-$100.
- Amount paid per month seems to be a big indicator in identifying customer churn.  


## Churn by Contract Type and Average Monthly Charges

![image](https://github.com/user-attachments/assets/b6d93091-069b-4bc4-a9cc-941eb0c9d824)

## Insights from box plots:
- More than 50% of customers who churned and were Month-to-month were paying above the median price ($64.95) of Non-Churn customers.
- Over 75% of customers who churned and were on a one year contract were paying on average above median price ($64.85) of Non-Churn customers.
- Same is true for customers who churned and were on a two year contract. 
- We can capture a great deal of customers who will churn by setting our threshold to the third quartile of each contract type for Non-Churn customers.


## Average Monthly Charges by Tenure (Months) and Churn status
![image](https://github.com/user-attachments/assets/020f944d-c862-4794-bcb4-e845b1c16261)


## Observation:
- Regardless of tenure, customers who churned were on average paying more than their counter parts who did not churn. 

### Exploring correlation between Salary, Distance and Decision to try new coffee selection



 


## Exploring how Salary plays a role in decision to purchase new potential selection of coffee



### Insights:
 


 # 3) Feature Engineering:

To prepare the dataset for machine learning, I performed several feature engineering steps to convert categorical data into a numerical format suitable for modeling:

🔢 1. One-Hot Encoding for Multi-Class Categorical Features
I used pandas.get_dummies() to transform multi-class categorical variables (such as 'InternetService', 'PaymentMethod', and 'Contract') into binary indicator variables. This method ensures that the model treats each category independently, without implying any ordinal relationship between them.

Example:
df_encoded = pd.get_dummies(df_encoded, columns=['InternetService', 'PaymentMethod', 'Contract'], drop_first=True)
This created new columns like:

- InternetService_DSL

- PaymentMethod_Electronic check

- Contract_Two year

✅ 2. Binary Encoding for Yes/No Features
For binary categorical features such as 'Partner', 'Dependents', 'PhoneService', 'PaperlessBilling', and 'Churn', I applied a simple mapping of 'Yes' to 1 and 'No' to 0. This encoding preserves the binary nature of these variables in a form that machine learning models can interpret directly.

Example:
binary_map = {'Yes': 1, 'No': 0}
df_encoded['Churn'] = df_encoded['Churn'].map(binary_map)

These steps ensured all features were fully numeric and compatible with scikit-learn and XGBoost, while preserving the semantic meaning of each variable.

# 4) Model Development:

## Models developed:

- Decision Tree - Entropy model - no max_depth
- Decision Tree - Gini impurity model - no max_depth
- Decision Tree - Entropy model - max depth 3
- Decision Tree - Gini impurity model - max depth 3
- Random Forest 


# 5) Model Evaluation: 
- Decision Tree - Entropy model - no max_depth: Accuracy = 0.9915966386554622
- Decision Tree - Gini impurity model - no max_depth: Accuracy = 0.9831932773109243
- Decision Tree - Entropy model - max depth 3: Accuracy = 0.907563025210084
- Decision Tree - Gini impurity model - max depth 3: Accuracy = 0.907563025210084
- Random Forest: Accuracy = 0.9663865546218487


## Conclusion
### Model Comparison Summary
After executing the Random Forest model, the results were nearly identical to those of my best-performing model (Model 4). While the Random Forest showed slightly higher metrics and was able to classify three new customers as "YES" for purchasing Hidden Farm Coffee, the overall predicted purchase percentage increased only marginally—remaining around 69.65%, which is still below the target threshold of 70%.


# My Recommendations for RR Diner Coffee Based on Decision Tree and Random Forest Analysis. 
- Based on the current data, I would advise RR Diner Coffee stakeholders not to proceed with the Hidden Farm deal at this time. The margin of uncertainty is too narrow, and the financial risk is too high given the minimal projected return.

- I recommend increasing marketing efforts within a 3-mile radius of each diner location. Customers living closer to the stores were significantly more likely to purchase Hidden Farm coffee. Targeted campaigns in these zones could help attract new loyal customers and boost future revenue.

- While this deal may not be ideal right now, it could become profitable in the future if the loyal customer base expands—especially within the high-conversion radius.

- Regardless of income level, proximity was a stronger predictor of purchase intent. Customers living within 3 miles were consistently more likely to buy Hidden Farm coffee.
