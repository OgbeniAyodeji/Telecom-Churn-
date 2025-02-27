# Telecom Customer Churn Analysis

## 📊 Project Overview

This project analyzes customer churn patterns in a telecommunications company using the CRISP-DM methodology. Understanding why customers leave is crucial for telecom businesses since acquiring new customers costs significantly more than retaining existing ones.

## 🎯 Business Objective

- Identify key factors influencing customer churn
- Analyze customer behavior patterns based on demographics, services, and contract types
- Provide data-driven recommendations for improving customer retention

## 📁 Dataset

The analysis uses the Telco Customer Churn dataset containing information about:
- Customer demographics (gender, senior citizen status, partners, dependents)
- Service details (phone, internet, TV streaming, online security, etc.)
- Contract information (type, billing method, charges)
- Churn status

## 🧹 Data Cleaning & Preparation

- Handled missing values in TotalCharges (11 records) by replacing with 0
- Ensured consistent formatting for categorical values (lowercase)
- Verified no duplicate records exist in the dataset
- Converted TotalCharges from object to numeric data type

```python
# Loading the dataset
import pandas as pd
import numpy as np

path = "./data/WA_Fn-UseC_-Telco-Customer-Churn.csv"
data = pd.read_csv(path)

# Make a copy of data
df = data.copy()

# Converting TotalCharges to numeric and handling missing values
df["TotalCharges"] = pd.to_numeric(df["TotalCharges"], errors="coerce")
print(f"Missing values in TotalCharges: {df['TotalCharges'].isnull().sum()}")

# Replace missing TotalCharges with 0
df["TotalCharges"].fillna(0, inplace=True)

# Check for duplicate customer IDs
duplicate_count = df.duplicated(subset=['customerID']).sum()
print(f"Duplicate records: {duplicate_count}")

# Convert categorical columns to consistent format (lowercase)
categorical_columns = df.select_dtypes(include=['object']).columns
df[categorical_columns] = df[categorical_columns].apply(
    lambda x: x.str.strip().str.lower() if x.dtype == "object" else x
)
```

## 🔍 Key Findings

### 1. Overall Churn Rate: 26.54%
A significant portion of customers are leaving the service, indicating retention issues.

```python
# Plot churn distribution
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 8))
sns.countplot(x=df["Churn"], palette=["blue", "red"])
plt.title("Churn Distribution")
plt.xlabel("Churn")
plt.ylabel("Count")
plt.show()

# Calculate churn percentage
churn_rate = df["Churn"].value_counts(normalize=True) * 100
print(f"Churn Rate: {churn_rate['yes']:.2f}%")
```

### 2. Contract Type Impact
- **Month-to-Month Contracts**: 42.7% churn rate
- **One Year Contracts**: 11.3% churn rate
- **Two Year Contracts**: 2.8% churn rate

Long-term contracts significantly improve customer retention.

```python
# Plot churn distribution by contract type
plt.figure(figsize=(8, 5))
sns.countplot(x="Contract", hue="Churn", data=df, palette=["blue", "red"])
plt.title("Churn Rate by Contract Type")
plt.xlabel("Contract Type")
plt.ylabel("Count")
plt.legend(title="Churn", labels=["No", "Yes"])
plt.show()

# Calculate churn percentages for each contract type
churn_by_contract = df.groupby("Contract")["Churn"].value_counts(normalize=True).unstack() * 100
print(churn_by_contract)
```



### 3. Internet Service Analysis
- **Fiber Optic Users**: 41.9% churn rate
- **DSL Users**: 19.0% churn rate
- **No Internet Service**: 7.4% churn rate

Fiber optic service has the highest churn rate despite being a premium offering.

### 4. Monthly Charges Correlation
- **Churned Customers**: Average $74.44/month
- **Retained Customers**: Average $61.27/month

Higher monthly charges correlate with increased likelihood of churn.

```python
# Boxplot of Monthly Charges by Churn
plt.figure(figsize=(8, 5))
sns.boxplot(x="Churn", y="MonthlyCharges", data=df, palette=["blue", "red"])
plt.title("Churn Rate by Monthly Charges")
plt.xlabel("Churn")
plt.ylabel("Monthly Charges")
plt.show()

# Calculate average monthly charges for churned vs. retained customers
monthly_charges_summary = df.groupby("Churn")["MonthlyCharges"].mean()
print(monthly_charges_summary)
```

 

### 5. Tenure Patterns
- **Churned Customers**: Average 18.0 months tenure
- **Retained Customers**: Average 37.6 months tenure

New customers are more likely to churn early, highlighting potential onboarding issues.

```python
# Plot distribution of tenure by churn
plt.figure(figsize=(8, 5))
sns.histplot(df[df["Churn"] == "no"]["tenure"], bins=30, color="blue", label="No Churn", kde=True)
sns.histplot(df[df["Churn"] == "yes"]["tenure"], bins=30, color="red", label="Churn", kde=True)
plt.title("Churn Rate by Tenure")
plt.xlabel("Tenure (Months)")
plt.ylabel("Count")
plt.legend()
plt.show()

# Calculate average tenure for churned vs. retained customers
tenure_summary = df.groupby("Churn")["tenure"].mean()
print(tenure_summary)
```


## 📈 Visualizations

The analysis includes various visualizations created using Matplotlib and Seaborn:

```python
# Summary statistics visualization for numerical features
fig, axes = plt.subplots(1, 3, figsize=(18, 5))

sns.histplot(df["tenure"], bins=30, kde=True, ax=axes[0], color="blue")
axes[0].set_title("Distribution of Tenure")

sns.histplot(df["MonthlyCharges"], bins=30, kde=True, ax=axes[1], color="green")
axes[1].set_title("Distribution of Monthly Charges")

sns.histplot(df["TotalCharges"], bins=30, kde=True, ax=axes[2], color="red")
axes[2].set_title("Distribution of Total Charges")

plt.tight_layout()
plt.show()
```

The analysis includes:
- Churn distribution across the dataset
- Contract type impact on churn
- Internet service type analysis
- Monthly charges comparison
- Tenure distribution for churned vs. retained customers

## 💡 Business Recommendations

### 1. Reduce Month-to-Month Contract Churn
- Offer discounts for long-term commitments
- Create easy upgrade paths to annual plans
- Implement loyalty rewards for month-to-month customers

### 2. Improve Fiber Optic Service Retention
- Investigate service quality issues
- Provide special incentives for fiber optic users
- Enhance technical support for premium services

### 3. Address High Monthly Charges
- Develop tiered pricing models
- Create customized plans for high-spending customers
- Implement loyalty programs with cost benefits

### 4. Enhance Customer Onboarding
- Provide personalized welcome experiences
- Offer early-stage discounts and support
- Implement check-ins during the first 6 months

## 🛠️ Technologies Used

- **Python** for data analysis
- **Pandas** for data manipulation
- **Matplotlib/Seaborn** for data visualization
- **Jupyter Notebook** for code development and documentation


## 📋 Dependencies

```python
# Required libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Dependencies list for requirements.txt
# pandas==1.5.3
# numpy==1.24.3
# matplotlib==3.7.1
# seaborn==0.12.2
```

## 📝 Future Work

- Develop predictive models to identify at-risk customers
- Perform customer segmentation for targeted retention strategies
- Conduct A/B testing on recommended retention tactics
- Analyze additional factors like customer service interactions