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

Here's a **table comparison** of the three clusters for easier readability:

| **Characteristic**            | **1: Moderate Credit Limit, Low Utilization**                      | **2: High-Income, High Credit Limit, Responsible Spenders**      | **3: Low Credit Limit, High Utilization**                         |
|--------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **Credit Limit**               | Moderate, suitable for modest spending.                                    | High, aligned with strong financial standing.                             | Low, reflecting constrained financial circumstances.                        |
| **Number of Transactions**     | Regular but moderate usage.                                                | Moderate usage with balanced spending habits.                             | Frequent transactions, indicating high card reliance.                       |
| **Transaction Amount**         | Small-scale purchases, reflecting financial restraint.                     | Higher-value purchases, indicating preference for premium items.          | Smaller transactions focused on essentials.                                 |
| **Revolving Balance**          | Low, showing controlled and disciplined credit usage.                      | Low, indicative of responsible credit management.                         | High, signaling significant reliance on credit.                             |
| **Income Category**            | Low to mid-income, with financial prudence.                                | Very high income, showcasing stability and capability.                    | Very low income, often facing financial stress.                             |
| **Age Group**                  | Predominantly aged 40-60, in later career or pre-retirement.                | Primarily aged 40-50, in prime earning years.                             | Mainly aged 40-60, managing responsibilities or nearing retirement.         |
| **Credit Utilization (%)**     | Minimal, reflecting conservative and efficient usage of credit.            | Very low, despite having significant credit capacity.                     | High, highlighting heavy dependence on available credit.                    |

This structured table provides a clear side-by-side comparison of the clusters for better understanding.

Here are actionable recommendations for each cluster based on the insights derived:

### **1: Moderate Credit Limit, Low Utilization Users with Low to Mid-Income**

| **Recommendation**                           | **Explanation**                                                                                  |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Encourage Credit Limit Increase**         | Since the users have a moderate credit limit but low utilization, offering them an option to increase their credit limit may encourage higher spending and improve their credit score. |
| **Introduce Rewards for Consistent Usage**  | Incentivize regular spending by introducing rewards programs that motivate increased transactions without pushing them into over-utilization. |
| **Promote Financial Education**             | Educate on the benefits of increasing credit utilization responsibly. As these users show restraint, they might benefit from understanding how higher utilization can positively affect their credit score. |
| **Cross-sell Low-Interest Loans or Products** | These users may appreciate the option to access personal loans or credit products with favorable interest rates, which would align with their modest financial behavior. |

### **2: High-Income, High Credit Limit, Responsible Spenders**

| **Recommendation**                           | **Explanation**                                                                                  |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Promote Premium Credit Products**         | Given their high income and low credit utilization, these users are ideal candidates for premium products like exclusive credit cards with benefits like cashbacks, travel perks, or VIP access. |
| **Offer Tailored Investment Products**      | Since they are financially stable, offer them investment options (like wealth management or retirement planning) to help grow their wealth. |
| **Introduce Exclusive Financial Tools**     | Provide tools or advisory services to optimize their wealth, tax benefits, or portfolio, which would appeal to their established financial expertise. |
| **Target with High-Value Offers**           | Engage them with exclusive offers, rewards, and experiences, leveraging their high spending potential without overburdening them with frequent offers. |

### **3: Low Credit Limit, High Utilization, Frequent Users with Very Low Income**

| **Recommendation**                           | **Explanation**                                                                                  |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Offer Credit Limit Increase with Caution** | Gradually increase the credit limit with guidance on how to use it responsibly, reducing the risk of users falling into a debt trap. |
| **Provide Debt Consolidation Options**      | Introduce debt consolidation services to help them manage high revolving balances more effectively, offering lower interest rates or manageable repayment terms. |
| **Promote Financial Counseling or Support**  | Offer free financial counseling to help users better manage their finances, especially with regard to budgeting and avoiding debt accumulation. |
| **Introduce Low-Cost, Essential Credit Products** | Provide access to low-cost, essential credit products or microloans with favorable terms, helping them meet their financial needs without overburdening them. |


---

## **Conclusion**

This project demonstrates how customer segmentation can guide personalized marketing strategies. By understanding customer behavior and tailoring offerings, credit card issuers can enhance customer satisfaction and loyalty.

--- 
