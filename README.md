# Customer-Churn-Prediction-Using-Machine-Learning


![image](https://github.com/user-attachments/assets/47c1934c-97bf-4d00-8b9c-ccf1ea3794e6)




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

1. [Go to Data Preprocesssing](#1-Data-Preprocessing)
2. [Go to Exploratory Data Analysis](#2-Exploratory-Data-Analysis)
3. [Go to Feature Engineering](#3-Feature-Engineering) 
4. [Go to Model Deployment](#4-Model-Deployment)
5. [Go to Model Evaluation](#5-Model-Evaluation)
6. [Go to Key Findings](#6-Key-Findings)
7. [Go to Business Suggestions](#7-Business-Recommendations) 


# 1. Data Preprocesssing
In the part of the project I loaded the data and checked for duplicate values and null values. Furthermore I explored the data types and discovered that all were numeric with the exception of two. 

df.head() and df.columns are used to explore the feature of the dataset and begin developing questions to explore during EDA. 


# 2. Exploratory Data Analysis

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

## Customer Distribution by Churn and Payment Method
![image](https://github.com/user-attachments/assets/5e51712b-4859-4bb1-bb22-7281141a49a2)

## Observation: Customer Churn and Payment Method
- Of the 15% of customers who churned used Electronic check as their payment method. This far exceeds the other categories of customers who churned which were almost identical. 

## Distribution of Churn and Dependents 
![image](https://github.com/user-attachments/assets/108e4d5c-e172-489f-995c-68f29a494646)

## Observation
- Of customers who did not churn 65% did not have dependents
- Of customers who did churn 82.5% did not have dependents.
- This shows customers who do not have dependents churn at slightly higher rates.

 


## Churn Distribution based on Gender and type of Internet Service 
![image](https://github.com/user-attachments/assets/1281bb34-4092-4389-b872-65858d121eca)

## Observations:
- Regardless of Gender customers were far more likely to churn if they had Fiber optic as an Internet service.
- This strongly suggest that customers with Fiber optic internet service were disatified by the quality.
- 35% of Females who did not churn had Fiber optic as an internet service.
- 70% of Females who DID churn had Fiber optic as an internet service. 

This clearly shows that having Fiber optic as an internet service has a high association with Churn. 


### Insights:
- Internet Service being Fiber optic is a key factor in determing customer churn.
- What could be the reason for this? Bad internet service?

## Churn and Online Security
![image](https://github.com/user-attachments/assets/0869ad7a-8865-4e77-97e2-ad0bf8fcf928)

## Observation
- A vast majority of customers who churned did not have Online Security.

## Churn Distribution and Tech Support 
![image](https://github.com/user-attachments/assets/a0f54676-10f2-48d4-97c3-0f2dedfa87ce)

## Observation
- Customers who churned were far more likely to have No tech support. 


## Correlation Matrix of Customer Churn Dataset
![image](https://github.com/user-attachments/assets/c1d20d55-c0e7-43db-8bba-b8a1f6971686)


### Observations:
Churn and Positive associations 

- Churn is positively corrlelated with Contract being Month-to-month at .40
- Churn is positively correlated with Payment Method being Electronic check at .30
- Churn is positively correlated with Internet being Fiber optic at .31 
- Internet Fiber Optic is highly postively correlated with higher Monthly charges at .79

Churn and Negative associations

- Churn is negatively correlated with Contract type being Two year at -.30
- Churn is negatively correlated with Contract type being One year at -.18
- Churn is negatively correlated with Not having internet service at -.23


## Key insights
- Monthly Charges are positively correlated with Internet being Fiber optic at .79. This answers the question as to why Customers with Fiber Optic internet service were churing at a higher rate, they are paying more per month. 
- Monthly Charges are negatively correlated with Internet being Fiber optic at -.79
This provides evidence that suggests that customers who have Fiber optic as a service will pay more per month. This is vital information since in EDA I discovered that customers who churned were paying more per month on average. 

- Senior Citizens are correlated with Internet Service being Fiber optic at .25
- Senior Citizens are correlated with Contratc type being Month-to-month at .14
- Senior Citizens are correlated with Payement method being Electronic check at .17


 # 3. Feature Engineering

To prepare the dataset for machine learning, I performed several feature engineering steps to convert categorical data into a numerical format suitable for modeling:

1. One-Hot Encoding for Multi-Class Categorical Features
I used pandas.get_dummies() to transform multi-class categorical variables (such as 'InternetService', 'PaymentMethod', and 'Contract') into binary indicator variables. This method ensures that the model treats each category independently, without implying any ordinal relationship between them.

Example:
df_encoded = pd.get_dummies(df_encoded, columns=['InternetService', 'PaymentMethod', 'Contract'], drop_first=True)
This created new columns like:

- InternetService_DSL

- PaymentMethod_Electronic check

- Contract_Two year

2. Binary Encoding for Yes/No Features
For binary categorical features such as 'Partner', 'Dependents', 'PhoneService', 'PaperlessBilling', and 'Churn', I applied a simple mapping of 'Yes' to 1 and 'No' to 0. This encoding preserves the binary nature of these variables in a form that machine learning models can interpret directly.

Example:
binary_map = {'Yes': 1, 'No': 0}
df_encoded['Churn'] = df_encoded['Churn'].map(binary_map)

These steps ensured all features were fully numeric and compatible with scikit-learn and XGBoost, while preserving the semantic meaning of each variable.

# 4. Model Development

## Models developed:

- Logistic Regression - Hyperparameter Tunning - Best Parameters {'C': 85.92819985213441, 'max_iter': 100, 'penalty': 'l2', 'solver': 'lbfgs'}
- Random Forest Classifier - Hyperparameter Tunning - Best Parameters: OrderedDict({'max_depth': 13, 'max_features': 'sqrt', 'min_samples_leaf': 1, 'min_samples_split': 2, 'n_estimators': 300})
- XGBoost Model - Hyperparameter Tunning - Best Params: {'subsample': 1.0, 'n_estimators': 100, 'min_child_weight': 1, 'max_depth': 10, 'learning_rate': 0.05, 'colsample_bytree': 0.6}


## SMOTE
- After evluating model metrics I decided to experiment with SMOTE to see if I could improve Recall scores for Churn. SMOTE stands for Synthetic Minority Over-sampling Technique. It's a powerful method used to address class imbalance in datasets. Since this dataset was composed of 26% churn customers it was imbalanced which means that my 'Churn' category was significantly underrepresented. 

Why use SMOTE? 
- I used SMOTE because it is particularly useful for binary classification problems when a model learns from imbalanced datasets the models could develop a bias for the majority class, in this case customers who did not churn. This could lead to poor performance in classifying minority class i.e. customer who did churn. 

## Model Insights: Feature Importance
The Random Forest model’s feature importance strongly reinforces the patterns uncovered during exploratory data analysis (EDA), providing a high degree of confidence in both the model and the underlying business insights.

![image](https://github.com/user-attachments/assets/91e42d8f-3499-4a01-a9af-e97327d21d15)

## Observations: Feature Importance
- The most imporant feature that the model used to predict customer Churn was type of Contract Month-to-month. This aligns with what I discovered during EDA (Month-to-month contracts are most likely to churn)
- The second most important feature is Tenure, This also align with what I discovered during EDA, The longer a customer has been with Telco the less likely they are to Churn. 
- Third most important features were Contract type being Two_year and Internet being Fiber optic.

## Top 5 Important Features XGBoost Model
![image](https://github.com/user-attachments/assets/7a425e1e-7c57-445a-81b4-0e4b04c735af)

## Observation: Feature Importance
- Top feature by far for XGBoost model was Contract_Month-to-month. This is reasurring sicne I came to a similar conclusion during EDA. 


## Top Feature - Contract_Month-to-month
- This was the most influential feature in predicting customer churn. It confirms what was observed in the EDA — customers on month-to-month contracts are significantly more likely to churn, likely due to the lack of long-term commitment or incentives to stay.

## Second Most Important Feature - Tenure 
- The longer a customer has been with Telco, the lower their likelihood of churning. This makes intuitive sense and aligns perfectly with the data: new or short-tenure customers are at higher risk of leaving.

## Other Key Features:
- InternetService_Fiber optic was also among the top contributors. As noted in the EDA, customers with Fiber Optic internet were more likely to churn, possibly due to higher costs or perceived service dissatisfaction.

These model-driven insights validate the EDA and highlight specific, high-leverage features that Telco can focus on to improve retention strategies.

# 5. Model Evaluation 

## Logistic Regression:

Test Accuracy: 0.7912400455062572



Classification Report:

              precision    recall  f1-score   support

           0       0.84      0.89      0.86      1300
           1       0.62      0.52      0.56       458

    accuracy                           0.79      1758
    macro avg      0.73      0.70      0.71      1758
    weighted avg   0.78      0.79      0.79      1758


 
## Random Forest Classifier

Test Accuracy: 0.7569296375266524



Classification Report:

              precision    recall  f1-score   support

           0       0.88      0.78      0.82      1033
           1       0.53      0.70      0.61       374

    accuracy                           0.76      1407
    macro avg       0.71      0.74     0.71      1407
    weighted avg    0.79      0.76     0.77      1407


## XGBoost Model 

Test ROC AUC: 0.8191861097162617
[[806 227]
 [120 254]]


 
              precision    recall  f1-score   support

           0       0.87      0.78      0.82      1033
           1       0.53      0.68      0.59       374

    accuracy                           0.75      1407
    macro avg      0.70      0.73      0.71      1407
    weighted avg   0.78      0.75      0.76      1407




# 6. Key Findings 

This customer churn analysis of Telco’s customer base uncovered several **critical insights** that can drive business strategy and customer retention efforts:

###  Key Findings

* **Churn Rate**: Approximately **27% of customers** in the dataset churned — a significant portion indicating potential revenue loss if not addressed.

* **Contract Type Matters**:

  * A staggering **89% of customers who churned were on Month-to-Month contracts**.
  * Only **2%** were on **1-year contracts**, and **1%** on **2-year contracts**.
    → 📉 **Shorter contracts strongly correlate with higher churn.**

* **Monthly Charges Are a Strong Predictor**:
  Customers who churned consistently paid **more per month**, regardless of contract type.

  * On **Month-to-Month contracts**, churned customers paid \~\$12 more than those who stayed.
  * On **2-Year contracts**, the gap increased to **\$26**.
    →  Higher charges are strongly associated with churn risk.

* **Fiber Optic Internet & Churn**:

  * Customers with **Fiber Optic** internet were **far more likely to churn**.
  * Among females who churned, **70% had Fiber Optic**, vs. **35%** of those who did not.
  * This may point to **pricing dissatisfaction or service quality issues**.

* **Lack of Support Services Increases Churn**:

  * Most customers who churned did **not have Online Security or Tech Support**.
  * These services might act as **"stickiness" features** and encourage retention.

* **Payment Method as a Signal**:

  * **Electronic check** is the most common payment method among churned customers (15%).
  * This may reflect a lower engagement or digital trust with the brand.

* **Dependents & Churn**:

  * **82.5% of churned customers had no dependents**, compared to 65% of those who stayed.
  * This may reflect differing priorities, risk aversion, or income stability.

# 7. Business Recommendations

1. **Target High-Risk Customers on Month-to-Month Contracts**

   * Offer incentives to **upgrade to longer-term contracts**.
   * Consider **discounts or loyalty programs** for high-paying month-to-month users.

2. **Investigate Fiber Optic Satisfaction**

   * Launch a **customer satisfaction survey** for Fiber Optic users.
   * Assess whether churn is due to **price sensitivity**, **service quality**, or both.

3. **Create Tiered Retention Offers Based on Monthly Charges**

   * Segment customers by price brackets (e.g., \$70–\$100/month) and contract type.
   * Tailor retention efforts (e.g., personalized discounts, added services) to high-paying users.

4. **Bundle Support Services (Online Security, Tech Support)**

   * Customers without these services churn more — offering them as part of packages may reduce churn.

5. **Optimize Onboarding for Electronic Check Users**

   * Explore payment experience friction or lack of auto-payment options.
   * Test **nudges** toward more stable digital payment methods.

6. **Deploy Predictive Thresholds**

   * Use churn probability thresholds based on **contract-type-specific quartiles** to preemptively flag at-risk customers.

---

This project not only highlights the power of predictive modeling in identifying churn risks but also demonstrates how **data-driven insights can directly inform retention strategy and operational decisions**.


