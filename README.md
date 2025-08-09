
#  Credit Card Financial Dashboard

This project develops an interactive credit card dashboard using SQL and Power BI, enabling stakeholders to explore real-time customer and transaction insights for better decision-making.

##  Objective
To build a comprehensive dashboard that:
- Integrates customer demographics with credit card behavior.
- Tracks key KPIs such as revenue, interest earned, activation, and delinquency rates.
- Supports data-driven business decisions through visual insights.

##  Dataset Overview
The project consists of two main datasets stored in SQL tables:

### 1️⃣ Customer Detail Table: `customer_detail`
Contains customer demographics and profile information.
```sql
CREATE TABLE customer_detail (
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

### 2️⃣ Credit Card Detail Table: `credit_detail`
Contains financial and behavioral transaction data.
```sql
CREATE TABLE credit_detail (
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
- Prepare CSV files.
- Create tables in SQL.
- Imported CSV files into SQL.
- Connected to **Power BI**  for analysis and visualization.


### DAX Measures
**Total Revenue**:
``` DAX
Total Revenue = 
SUM('credit_detail'[Total_Trans_Amt]) + 
SUM(' credit_detail'[Annual_Fees]) + 
SUM('credit_detail'[Interest_Earned])
```

**Age Group Column**:
``` DAX
AgeGroup = SWITCH(
    TRUE(),
    'customer_detail'[Customer_Age] < 30, "20-30",
    'customer_detail'[Customer_Age] < 40, "30-40",
    'customer_detail'[Customer_Age] < 50, "40-50",
    'customer_detail'[Customer_Age] >= 60, "60+"
)
```

```
current_week_revenue = CALCULATE(
    SUM('credit_detail'[revenue]),
    FILTER(
        ALL('credit_detail'),
        'credit_detail'[week_num2] = MAX('public credit_detail'[week_num2])))

```

```
weekly_revenue = DIVIDE(([current_week_revenue]-[previous_week_revenue]), [previous_week_revenue])

```

##Power BI Dashboard Features

### KPIs
| Metric                        | Value        |
|------------------------------|--------------|
| **Total Revenue**            | `$55M`       |
| **Transaction Volume**       | `$45M`       |
| **Interest Earned**          | `$7.8M`      |
| **Activation Rate**          | `57%`        |
| **Delinquency Rate**         | `6%`         |

## Key Insights
- **Weekly Change `52nd Week`**
  - Revenue decreased by `12.8%`. That is `51st week $1070439` and `52nd week $933134`
  - Transaction decreased from `51st week $865275` to `52nd week $748677`
  - Income decreased from `51st week $11075808` to `52nd week $9883404`
  - Customer decreased from `51st week 12587` to `52nd week 11203`
- **Gender**:  
  - Males contribute `$30M` revenue, Females `$25M`.
- **Card Type**:  
  - Blue and Silver cards generate over **94%** of total transactions.
- **Geography**:  
  - Texas, New York, and California together account for `$38M` **69%** of revenue.

## Power BI
- Power BI dashboard built with live SQL connection.
- Published dashboard enables stakeholder-driven self-service exploration.

##  Tools Used
-  SQL 
-  Power BI 
-  DAX
-  CSV


##  Contact
Created by **[Dilip Adhikari]**   
[LinkedIn](https://www.linkedin.com/in/dilip-adhikari/)  



