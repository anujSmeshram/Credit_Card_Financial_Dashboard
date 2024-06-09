# Project Title

# Credit_Card_Financial_Dashboard
Power BI Dashboard

### Project Description
This project aims to develop a comprehensive credit card weekly dashboard that provides real-time insights into key performance metrics and trends. The dashboard enables stakeholders to monitor and analyze credit card operations effectively.

### Features
- Real-time insights into key performance metrics.
- Trend analysis of credit card operations.
- Easy-to-use weekly dashboard interface.

### Technologies Used
- **Power BI**: For creating the dashboard.
- **DAX**: For writing data analysis expressions.
- **SQL**: For database management and querying.


### DAX Queries
#### AgeGroup and IncomeGroup
```dax
AgeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[customer_age] < 30, "20-30",
    'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
    'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
    'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
    'public cust_detail'[customer_age] >= 60, "60+",
    "unknown"
)

IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)



week_num2 = WEEKNUM('public cc_detail'[week_start_date])



Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]



Current_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)



Previous_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
    )
)
