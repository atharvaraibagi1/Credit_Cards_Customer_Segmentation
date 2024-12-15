# Credit Card Customer Segmentation using K-Means

This repository contains a project for credit card customer segmentation using K-Means clustering, leveraging data from Kaggle. The dataset used for this project is focused on predicting customer attrition in credit card services, with a variety of features representing customer activity, financial behavior, card usage patterns, and demographic details.

---

## **Dataset**
The dataset used in this project is sourced from Kaggle:  
[Credit Card Customer Attrition Dataset](https://www.kaggle.com/datasets/thedevastator/predicting-credit-card-customer-attrition-with-m).

### **Dataset Overview**
The dataset contains various attributes about credit card customers, such as demographic information, transaction details, card usage behavior, and customer activity. Key columns in the dataset include:

- **Customer_Age**: Age of the customer.
- **Months_on_book**: The number of months the customer has been with the bank.
- **Credit_Limit**: Credit limit assigned to the customer.
- **Total_Trans_Amt**: Total transaction amount in the past year.
- **Total_Trans_Ct**: Total number of transactions in the past year.
- **Total_Revolving_Bal**: The total revolving balance.
- **Avg_Open_To_Buy**: The average available credit.

### **Data Exploration and Cleaning**
The data was loaded and thoroughly explored to understand its structure and identify missing values. 
---

## **Feature Engineering**

To better understand the customer segments and make the clustering more meaningful, various new features were engineered, which can be categorized as follows:

### **Customer Activity**
| Feature                         | Formula                                      |
|----------------------------------|----------------------------------------------|
| `Months_Active_12_mon`          | `12 - Months_Inactive_12_mon`                |
| `Contacts_per_Month`            | `Contacts_Count_12_mon / Months_Active_12_mon` |

### **Financial Behavior Features**
| Feature                         | Formula                                      |
|----------------------------------|----------------------------------------------|
| `revolving_balance_by_credit_limit` | `Total_Revolving_Bal / Credit_Limit`         |
| `Spending_Ratio`                | `Total_Trans_Amt / Credit_Limit`             |

### **Card Usage Behaviour**
| Feature                         | Formula                                      |
|----------------------------------|----------------------------------------------|
| `card_usage_count_per_month`    | `Total_Trans_Ct / Months_on_book`            |
| `card_usage_amount_per_month`   | `Total_Trans_Amt / Months_on_book`           |
| `Remaining_Credit`              | `Credit_Limit - Total_Revolving_Bal`         |

### **Age-Based Features**
| Feature                         | Formula                                      |
|----------------------------------|----------------------------------------------|
| `Dependents_by_Age`             | `(Dependent_count+1) / Customer_Age`         |
| `Customer_Usage%_of_Age`        | `(Months_on_book / 12) / Customer_Age`      |

### **Income-Based Features**
| Feature                         | Formula                                      |
|----------------------------------|----------------------------------------------|
| `Income_per_Dependent`          | `Income / (Dependent_count + 1)`              |
| `Credit_Limit_%_of_Income`      | `Credit_Limit / Income`                      |

### **Relationship Features**
| Feature                         | Formula                                      |
|----------------------------------|----------------------------------------------|
| `Relationship_Per_Year`         | `Total_Relationship_Count / (Months_on_book * 12)` |
| `Credit_per_Relationship`       | `Credit_Limit / Total_Relationship_Count`    |

### **Transaction Amount Features**
| Feature                         | Formula                                      |
|----------------------------------|----------------------------------------------|
| `Transaction_Intensity`         | `Total_Trans_Amt / Total_Trans_Ct`           |
| `Transaction_Proportion`        | `Total_Trans_Amt / Credit_Limit`             |

---

## **K-Means Clustering**

### **Elbow Method**
The optimal number of clusters was determined using the elbow plot method, which showed that 3 clusters best represented the data.

### **Clusters Identified**
After performing K-Means clustering, the dataset was divided into three distinct clusters based on customer behavior:

- **High Credit Utilization Customers**
  - **Key Traits**:
    - High revolving balance-to-credit limit (0.618906).
    - High spending ratio (0.319330).
    - Low remaining credit (0.031564).
  - **Demographic Insights**: Middle-aged customers with mid-to-high incomes. They manage their spending responsibly and depend heavily on credit limits.
  - **Behavioral Summary**: Frequent card users who maintain a high revolving balance.

- **Balanced Usage Customers**
  - **Key Traits**:
    - Moderate revolving balance-to-credit limit (0.117687).
    - Moderate spending ratio (0.177295).
    - Moderate remaining credit (0.169929).
  - **Demographic Insights**: Middle-aged or younger customers with moderate incomes. They prioritize financial stability and use credit cards cautiously.
  - **Behavioral Summary**: Low-risk users with high financial discipline.

- **Conservative Users**
  - **Key Traits**:
    - Very low revolving balance-to-credit limit (0.044101).
    - Very low spending ratio (0.036409).
    - Extremely high remaining credit (0.738300).
  - **Demographic Insights**: Younger or mid-aged individuals with low-to-mid incomes. They have high borrowing capacity but prefer conservative spending.
  - **Behavioral Summary**: They tend to pay off balances in full, avoiding interest accumulation.

---

## **New Clusters with Age and Income Bins**
By binning customers based on age and income, additional customer segments were created:

| Cluster Name                                       | Customer Count |
|---------------------------------------------------|----------------|
| Mid Age, Low Income, Balanced Usage Customers     | 2341           |
| Mid Age, Low Income, High Credit Utilization      | 1976           |
| Mid Age, Good Income, Balanced Usage Customers    | 1093           |
| Young, Low Income, Balanced Usage Customers       | 812            |
| Mid Age, Good Income, Conservative Users          | 754            |
| Young, Low Income, High Credit Utilization        | 730            |
| Mid Age, Good Income, High Credit Utilization     | 363            |
| Mid Age, High Income, Conservative Users          | 335            |
| Young, Good Income, Balanced Usage Customers      | 322            |
| Young, Good Income, Conservative Users            | 204            |
| Mid Age, High Income, Balanced Usage Customers    | 203            |
| Mid Age, Low Income, Conservative Users           | 201            |
| Old Age, Low Income, Balanced Usage Customers     | 177            |
| Old Age, Low Income, High Credit Utilization      | 140            |
| Young, Good Income, High Credit Utilization       | 131            |
| Young, Low Income, Conservative Users             | 72             |
| Young, High Income, Conservative Users            | 61             |
| Mid Age, High Income, High Credit Utilization     | 59             |
| Young, High Income, Balanced Usage Customers      | 49             |
| Old Age, Good Income, Balanced Usage Customers    | 40             |
| Old Age, Good Income, Conservative Users          | 18             |
| Young, High Income, High Credit Utilization       | 16             |
| Old Age, Low Income, Conservative Users           | 14             |
| Old Age, Good Income, High Credit Utilization     | 12             |
| Old Age, High Income, Balanced Usage Customers    | 2              |
| Old Age, High Income, Conservative Users          | 2              |

---

## **Actionable Recommendations for Each Cluster**

### **High Credit Utilization Customers**
- **Premium Benefits Programs**: Offer high-value perks like travel rewards or exclusive events.
- **Investment and Savings Plans**: Provide investment advisory services and competitive interest savings.
- **Encourage Controlled Spending**: Offer cashback or discounts in selected categories to increase card usage.

### **Balanced Usage Customers**
- **Debt Management Programs**: Provide personalized repayment plans or interest rate reductions.
- **Spending Control Incentives**: Offer cashback or rewards for staying within credit limits.
- **Financial Education**: Promote responsible credit usage and improving credit health.

### **Conservative Users**
- **Upsell Financial Products**: Introduce co-branded cards and upgrade opportunities with better benefits.
- **Credit Utilization Education**: Educate about the benefits of credit card usage for building credit scores.
- **Loyalty Programs**: Implement rewards for moderate, disciplined usage, like dining or fuel discounts.

---

## **Conclusion**

This project demonstrates how clustering credit card customers into distinct profiles can provide actionable insights for better targeting and personalized marketing strategies. The segmentation helps financial institutions develop customized offers, promotions, and educational resources that align with each segment’s unique behavior and financial needs.
