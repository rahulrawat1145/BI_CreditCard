# CREDIT CARD DASHBOARD

### Objective:
Creation of two comprehensive credit card dashboards, one reflecting credit card customer report and other reflecting credit card transaction report. Each Dashboard features performance metrics like Revenue by Expenditure, Revenue by Customer Job and Total Revenue etc. The dashboard shold provide realtime insights into key performance metrics and trends, enabling stakeholder to monitor and analyze credit card operations effectively.

### About the Dataset:
The dataset is available to download in the repository. The dataset is divided into two files, one for customer details and other for credit card details. Each file has around 18 cloumns and nearly 11000 rows. 

### About the Analysis:

The analysis begins with creating a database in MySQL. The sql file is available to download in the repository. The following codes were used to create a database:
```
-- Creating the Database

CREATE DATABASE credit_card_db;
USE credit_card_db;

--  Creating tables

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
After creation of the database, Microsoft Power BI was used to perform data analysis on multiple layers information. Some DAX codes used to create column and measures are as under:

```
IncomeGroup = SWITCH(
     TRUE(),
     cust_detail[Income] <35000, "Low",
     cust_detail[Income] >= 35000 && cust_detail[Income] < 70000, "Med",
     cust_detail[Income] >= 70000, "High",
     "unknown"
     )
Current_week_revenue = CALCULATE(
    SUM(cc_detail[Revenue]),
    FILTER(
        ALL('cc_detail'),
        'cc_detail'[Week_num2] = MAX(cc_detail[Week_num2])
    )
)

```
After analysis two dashboards were made. The dashboard is available to download in the main repository. The screenshot of the dashboards are as under:
![image1](https://github.com/rrawat1145/BI_CreditCard/blob/main/Screenchot/1%20(1).png?raw=true)

And

![image2](https://github.com/rrawat1145/BI_CreditCard/blob/main/Screenchot/1%20(2).png?raw=true)

