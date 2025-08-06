
#  Credit Card Financial Dashboard

This project develops an interactive credit card dashboard using SQL and Power BI, enabling stakeholders to explore real-time customer and transaction insights for better decision-making.

##  Objective
To build a comprehensive dashboard that:
- Integrates customer demographics with credit card behavior.
- Tracks key KPIs such as revenue, interest earned, activation, and delinquency rates.
- Supports data-driven business decisions through visual insights.

##  Dataset Overview
The project consists of two main datasets stored in SQL tables:

### 1️⃣ Customer Detail Table: `cust_detail`
Contains customer demographics and profile information.
```sql
CREATE TABLE cust_detail (
    Client_Num INT,
    Customer_Age INT,
    Gender VARCHAR(5),
    Dependent_Count INT,
    Education_Level VARCHAR(50),
    Marital_Status VARCHAR(20),
    State_cd VARCHAR(50),
    Zipcode VARCHAR(20),
    Car_Owner VARCHAR(5),
    House_Owner VARCHAR(5),
    Personal_Loan VARCHAR(5),
    Contact VARCHAR(50),
    Customer_Job VARCHAR(50),
    Income INT,
    Cust_Satisfaction_Score INT
);
```

### 2️⃣ Credit Card Detail Table: `cc_detail`
Contains financial and behavioral transaction data.
```sql
CREATE TABLE cc_detail (
    Client_Num INT,
    Card_Category VARCHAR(20),
    Annual_Fees INT,
    Activation_30_Days INT,
    Customer_Acq_Cost INT,
    Week_Start_Date DATE,
    Week_Num VARCHAR(20),
    Qtr VARCHAR(10),
    current_year INT,
    Credit_Limit DECIMAL(10,2),
    Total_Revolving_Bal INT,
    Total_Trans_Amt INT,
    Total_Trans_Ct INT,
    Avg_Utilization_Ratio DECIMAL(10,3),
    Use_Chip VARCHAR(10),
    Exp_Type VARCHAR(50),
    Interest_Earned DECIMAL(10,3),
    Delinquent_Acc VARCHAR(5)
);
```

##  Data Pipeline & Integration
- Data is stored in **PostgreSQL Server**.
- Imported via `.CSV` files.
- Joined on `Client_Num` to link customer and transaction details.
- Connected to **Power BI**  for analysis and visualization.


### DAX Measures
**Total Revenue**:
``` DAX
Total Revenue = 
SUM('cc_detail'[Total_Trans_Amt]) + 
SUM('cc_detail'[Annual_Fees]) + 
SUM('cc_detail'[Interest_Earned])
```

**Age Group Column**:
``` DAX
AgeGroup = SWITCH(
    TRUE(),
    'cust_detail'[Customer_Age] < 30, "20-30",
    'cust_detail'[Customer_Age] < 40, "30-40",
    'cust_detail'[Customer_Age] < 50, "40-50",
    'cust_detail'[Customer_Age] >= 60, "60+"
)
```

##Power BI Dashboard Features

### KPIs
| Metric                        | Value        |
|------------------------------|--------------|
| **Total Revenue**            | `$57M`       |
| **Transaction Volume**       | `$45M`       |
| **Interest Earned**          | `$8M`        |
| **Activation Rate**          | `55%`        |
| **Delinquency Rate**         | `5%`         |

## Key Insights
- **Gender**:  
  - Males contribute `$31M` revenue, Females `$26M`.
- **Card Type**:  
  - Blue and Silver cards generate over **90%** of total transactions.
- **Geography**:  
  - Texas, New York, and California together account for **68%** of revenue.

## Power BI
-  Power BI dashboard built with live SQL connection.
- Offers filters on card type, customer segment, and geography.
- Published dashboard enables stakeholder-driven self-service exploration.

##  Tools Used
-  SQL 
-  Power BI 
-  DAX
-  CSV


##  Contact
Created by **[Dilip Adhikari]**   
[LinkedIn](https://www.linkedin.com/in/dilip-adhikari/)  



