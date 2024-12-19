# Credit Card Customer Segmentation using K-Means

This repository contains a project for credit card customer segmentation using K-Means clustering, leveraging data from Kaggle. The dataset focuses on predicting customer attrition in credit card services, with a variety of features representing customer activity, financial behavior, card usage patterns, and demographic details.

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

---

## **Feature Engineering**

Several new features were created to enhance clustering and understand customer segments better:

### **Customer Activity**
| Feature                     | Formula                                         |
|-----------------------------|-------------------------------------------------|
| `Months_Active_12_mon`      | `12 - Months_Inactive_12_mon`                   |
| `Contacts_per_Month`        | `Contacts_Count_12_mon / Months_Active_12_mon` |

### **Financial Behavior Features**
| Feature                           | Formula                                      |
|-----------------------------------|----------------------------------------------|
| `revolving_balance_by_credit_limit` | `Total_Revolving_Bal / Credit_Limit`         |
| `Spending_Ratio`                  | `Total_Trans_Amt / Credit_Limit`             |
| `payment_left_of_credit_limit_%`  | `Total_Revolving_Bal / Credit_Limit`         |

### **Card Usage Behaviour**
| Feature                           | Formula                                      |
|-----------------------------------|----------------------------------------------|
| `card_usage_count_per_month`      | `Total_Trans_Ct / Months_on_book`            |
| `card_usage_amount_per_month`     | `Total_Trans_Amt / Months_on_book`           |
| `Remaining_Credit`                | `Credit_Limit - Total_Revolving_Bal`         |
| `total_card_usage_of_credit_limit_%` | `Total_Trans_Amt / Credit_Limit`          |

### **Age-Based Features**
| Feature                           | Formula                                      |
|-----------------------------------|----------------------------------------------|
| `Dependents_by_Age`               | `(Dependent_count+1) / Customer_Age`         |
| `Customer_Usage%_of_Age`          | `(Months_on_book / 12) / Customer_Age`      |

### **Income-Based Features**
| Feature                           | Formula                                      |
|-----------------------------------|----------------------------------------------|
| `Income_per_Dependent`            | `Income / (Dependent_count + 1)`              |
| `Credit_Limit_%_of_Income`        | `Credit_Limit / Income`                      |

### **Transaction Features**
| Feature                           | Formula                                      |
|-----------------------------------|----------------------------------------------|
| `amount_per_trans`                | `Total_Trans_Amt / Total_Trans_Ct`           |
| `Transaction_Intensity`           | `Total_Trans_Amt / Total_Trans_Ct`           |
| `Transaction_Proportion`          | `Total_Trans_Amt / Credit_Limit`             |

---

## **K-Means Clustering**

### **Elbow Method**
The optimal number of clusters was determined using the elbow plot method, which showed that **3 clusters** best represented the data.

### **Clusters Identified**

### 1. **Moderate Credit Limit, Low Utilization Users with Low to Mid-Income**  
- **Credit Limit:** Customers in this group typically have a moderate credit limit, suited to their modest spending patterns.  
- **Card Usage:** They demonstrate regular usage with a manageable number of transactions, focusing on small-scale purchases.  
- **Transaction Behavior:** The average transaction value is modest, reflecting careful financial habits and an inclination towards smaller expenses.  
- **Revolving Balance:** These users maintain low revolving balances, highlighting a disciplined approach to credit usage.  
- **Income Category:** Falling within the low to mid-income bracket, this group reflects financial prudence and restraint.  
- **Age Group:** Predominantly aged between 40 and 60, they are often in the later stages of their careers or approaching retirement.  
- **Credit Utilization:** The percentage of credit used is minimal, reflecting conservative spending and efficient credit management.  

---

### 2. **High-Income, High Credit Limit, Low Utilization, Responsible Spenders**  
- **Credit Limit:** This cluster comprises customers with significantly high credit limits, aligned with their robust financial standing.  
- **Card Usage:** These individuals use their cards moderately, emphasizing quality over quantity in their transactions.  
- **Transaction Behavior:** Purchases tend to be of higher value, showcasing a preference for premium products and services.  
- **Revolving Balance:** They maintain low revolving balances, indicative of responsible credit management and financial discipline.  
- **Income Category:** Representing a very high-income group, these customers exhibit financial stability and spending power.  
- **Age Group:** Typically aged between 40 and 50, they are in their prime earning years, balancing professional and personal commitments.  
- **Credit Utilization:** Their utilization rate is exceptionally low, underlining a cautious approach to credit despite substantial financial capability.  

---

### 3. **Low Credit Limit, High Utilization, Frequent Users with Very Low Income**  
- **Credit Limit:** Customers in this segment operate with low credit limits, often reflecting their constrained financial circumstances.  
- **Card Usage:** They frequently use their cards, relying heavily on credit for daily transactions.  
- **Transaction Behavior:** Purchases are smaller in value, indicating a focus on essential or budgeted expenses.  
- **Revolving Balance:** High revolving balances are common, highlighting a reliance on credit for sustaining financial needs.  
- **Income Category:** This group represents very low-income earners, often experiencing financial stress or limited earning potential.  
- **Age Group:** Aged predominantly between 40 and 60, they are often managing household responsibilities or transitioning towards retirement.  
- **Credit Utilization:** Their credit usage is high, reflecting a heavy dependence on available credit and potential financial challenges.  

Let me know if further refinements are needed!

## **Actionable Recommendations for Each Cluster**

### **Moderate Credit Users**
- Encourage increased credit card usage through cashback offers or dining rewards.
- Introduce financial wellness programs to promote responsible spending habits.

### **Premium Low Utilization Customers**
- Offer exclusive benefits, such as luxury rewards or premium experiences.
- Introduce high-value co-branded cards with additional perks to incentivize higher spending.

### **High Utilization Frequent Users**
- Provide debt management support with lower interest repayment plans.
- Educate on credit utilization's impact on credit scores and offer small credit line increments.

---

## **Conclusion**

This project demonstrates how customer segmentation can guide personalized marketing strategies. By understanding customer behavior and tailoring offerings, credit card issuers can enhance customer satisfaction and loyalty.

--- 
