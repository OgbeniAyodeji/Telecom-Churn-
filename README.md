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

## 🔍 Key Findings

### 1. Overall Churn Rate: 26.54%
A significant portion of customers are leaving the service, indicating retention issues.

### 2. Contract Type Impact
- **Month-to-Month Contracts**: 42.7% churn rate
- **One Year Contracts**: 11.3% churn rate
- **Two Year Contracts**: 2.8% churn rate

Long-term contracts significantly improve customer retention.

### 3. Internet Service Analysis
- **Fiber Optic Users**: 41.9% churn rate
- **DSL Users**: 19.0% churn rate
- **No Internet Service**: 7.4% churn rate

Fiber optic service has the highest churn rate despite being a premium offering.

### 4. Monthly Charges Correlation
- **Churned Customers**: Average $74.44/month
- **Retained Customers**: Average $61.27/month

Higher monthly charges correlate with increased likelihood of churn.

### 5. Tenure Patterns
- **Churned Customers**: Average 18.0 months tenure
- **Retained Customers**: Average 37.6 months tenure

New customers are more likely to churn early, highlighting potential onboarding issues.

## 📈 Visualizations

The analysis includes various visualizations:
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

## 🚀 How to Run

```bash
# Clone the repository
git clone https://github.com/yourusername/telecom-churn-analysis.git

# Navigate to the project directory
cd telecom-churn-analysis

# Install required packages
pip install -r requirements.txt

# Run the Jupyter notebook
jupyter notebook Telecom_Customer_Churn_Analysis.ipynb
```

## 📝 Future Work

- Develop predictive models to identify at-risk customers
- Perform customer segmentation for targeted retention strategies
- Conduct A/B testing on recommended retention tactics
- Analyze additional factors like customer service interactions

