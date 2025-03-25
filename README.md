# Customer-Segmentation-UCI-ML - February 28, 2025

## **1️⃣ Project Overview**

### **🎯 Goal**

- Understand **customer behavior** using **RFM analysis** and **K-Means clustering**.
- Identify **VIPs, loyal customers, occasional buyers, and lost customers**.
- Provide **data-driven marketing and retention strategies**.

### **📊 Dataset**

- **Source:** UCI Online Retail Dataset.
- **Key Features:**
    - `InvoiceDate` → Purchase date.
    - `CustomerID` → Unique customer identifier.
    - `Quantity` → Number of products bought.
    - `UnitPrice` → Price per unit.
    - `Country` → Customer’s country.

---

## **2️⃣ Methodology**

### **📌 Step 1: Data Cleaning & Preprocessing**

- Removed **missing Customer IDs**.
- Converted **dates to datetime format**.
- Scaled and transformed data for clustering.

### **📌 Step 2: RFM Analysis (Recency, Frequency, Monetary)**

| **Metric** | **Meaning** | **How We Calculated It** |
| --- | --- | --- |
| **Recency** | How recently did the customer purchase? | Days since last purchase. |
| **Frequency** | How often does the customer buy? | Total number of transactions. |
| **Monetary** | How much has the customer spent? | Total revenue per customer. |

🔹 **Customers were grouped into RFM quartiles (1-4), higher is better.**

### **📌 Step 3: K-Means Clustering (K=5)**

- Used **Elbow Method** to determine **K=5**.
- Standardized **RFM values** before clustering.
- Assigned customers into **5 distinct groups**.

---

## **3️⃣ Cluster Insights & Business Strategy**

| **Cluster** | **Count** | **Customer Behavior** | **Business Strategy** |
| --- | --- | --- | --- |
| **3 - VIP Customers** | 5 | Very recent buyers, frequent shoppers, highest spenders. | **Loyalty programs, premium support, exclusive deals.** |
| **2 - Super Loyal Customers** | 4 | Most active, highest purchase frequency. | **Subscription models, automatic re-order offers.** |
| **4 - Frequent Buyers** | 241 | Shop regularly, moderate spending. | **Personalized recommendations, targeted promotions.** |
| **1 - Occasional Buyers** | 3050 | Buy sometimes, low spenders. | **Re-engagement emails, discounts, product recommendations.** |
| **0 - Lost Customers** | 1072 | Haven’t bought in a long time, lowest spenders. | **Win-back campaigns, special limited-time offers.** |

---

## 📂 Resources & Code Snippets

📒 **Colab Notebook:** https://colab.research.google.com/drive/1sKraqzdhETEoO3ahu7v-HqAUtCmYTUzQ?usp=sharing

📄 **Key Snippets:**

```
from sklearn.cluster import KMeans

# Re-scale only valid customers
rfm_scaled_clean = scaler.fit_transform(rfm_clean[['Recency', 'Frequency', 'Monetary']])

# Apply K-Means Clustering
optimal_k = 5  # I chose 5 (tested 3, 4, 6) based on elbow method
kmeans = KMeans(n_clusters=optimal_k, random_state=42, n_init=10)
clusters = kmeans.fit_predict(rfm_scaled_clean)

# Add cluster labels to a new DataFrame
rfm_clean = rfm_clean.copy()
rfm_clean['Cluster'] = clusters  # Now, 'Cluster' column exists

# Show cluster counts
print(rfm_clean['Cluster'].value_counts())
```

---

## **4️⃣ TL;DR (Summary)**

### **📌 Key Takeaways**

✔ **VIP & Loyal customers contribute most revenue** → Retention is crucial.

✔ **Lost customers are inactive for ~250+ days** → Need win-back campaigns.

✔ **Super Loyal Customers buy most frequently** → Subscription models work.

✔ **Frequent buyers need engagement nudges** → Personalized recommendations.

✔ **Data-driven marketing improves retention & revenue**.
