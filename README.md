💳 Credit Card Financial Dashboard | Power BI Project

Credit cards are more than payment tools — they’re behavioral data streams.
This dashboard captures those signals and converts them into actionable financial insights.

The Credit Card Financial Dashboard provides a weekly view of revenue, transactions, customer activity, and delinquency trends. Built with Power BI and fueled by SQL data, it helps financial analysts and product managers track portfolio performance and customer health in real time.

🎯 Purpose & Business Problem

Financial institutions deal with thousands of transactions every week — identifying revenue drivers, high-risk accounts, and underperforming products in time is critical.

This project was built to:

Monitor weekly revenue, transactions, and customer activity.

Compare current vs previous week performance.

Identify which states, customer segments, and card categories contribute most to profits.

Support data-driven decisions for credit product teams and risk analysts.

🧩 Data Model & Sources
File	Description
credit_card.csv	Base transaction data – card type, spend, interest, delinquency
customer.csv	Customer demographics and profile info
cc_add.csv	Week 53 incremental transaction data
cust_add.csv	Week 53 incremental customer data
SQL Query - Financial Dashboard Data.sql	Database schema & COPY commands to load CSVs into SQL
Credit.Card.Financial.Dashboard.pbix	Power BI report with data model, DAX, and visuals

Data was imported from PostgreSQL using Power BI’s connector after execution of SQL setup scripts.

🧱 SQL Setup
-- Create database and tables
CREATE DATABASE ccdb;
CREATE TABLE cc_detail (...);
CREATE TABLE cust_detail (...);

-- Load base CSVs
COPY cc_detail FROM 'D:\credit_card.csv' CSV HEADER;
COPY cust_detail FROM 'D:\customer.csv' CSV HEADER;

-- Append Week 53 data
COPY cc_detail FROM 'D:\cc_add.csv' CSV HEADER;
COPY cust_detail FROM 'D:\cust_add.csv' CSV HEADER;

⚙️ Tech Stack

SQL (PostgreSQL) – data ingestion and schema management

Power BI Desktop – modeling, DAX, and visualization

Power Query (M) – ETL for data cleaning and merging

DAX – calculations for revenue, week-over-week (WoW) growth, and segmentation

📊 Dashboard Highlights
KPI	Value / Metric
Total Revenue	$57M
Interest Earned	$8M
Total Transaction Amount	$46M
Activation Rate	57.5 %
Delinquent Rate	6.06 %
Top Performing States	TX, NY, CA (68 % of total revenue)

Key Insights:

🔹 Revenue up +28.8% week-over-week in Week 53.

🔹 Male customers contributed $31M, females $26M.

🔹 Blue and Silver cards accounted for 93% of all transactions.

🔹 High-income customers have the lowest delinquency rates.

🧮 Analytical Logic
Calculation	DAX / SQL Expression
Age Group	SWITCH(TRUE(), [Age]<30,"20-30", [Age]<40,"30-40", [Age]<50,"40-50", [Age]<60,"50-60", "60+")
Income Group	SWITCH(TRUE(), [Income]<35000,"Low", [Income]<70000,"Med", "High")
Revenue	Annual Fees + Total_Trans_Amt + Interest_Earned
Current Week Revenue	CALCULATE(SUM([Revenue]), FILTER(ALL(cc_detail), [Week_Num] = MAX([Week_Num])))
Previous Week Revenue	CALCULATE(SUM([Revenue]), FILTER(ALL(cc_detail), [Week_Num] = MAX([Week_Num])-1))
🖥️ Dashboard Preview

Revenue & Transaction Overview


Customer Insights View


🧠 What I Learned

Combining SQL and Power BI gives full control over data pipelines and performance.

DAX time intelligence (like WoW) enables true financial trend storytelling.

Cross-highlighting between customer and transaction views creates instant cause-effect visibility.

Translating raw numbers into insights demands a blend of logic, design, and empathy for the user.
