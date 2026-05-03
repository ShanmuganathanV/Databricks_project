🛒 Retail Sales Analytics — End-to-End Data Engineering Project

This project demonstrates a complete Medallion Architecture (Bronze → Silver → Gold) pipeline built on Databricks (Free Edition) using PySpark.

The dataset consists of one CSV file (orders) and one JSON file (customer details). Using these raw files, the pipeline:

Ingests data into Bronze layer

Cleans & transforms using PySpark (Silver layer)

Creates aggregated analytical tables (Gold layer)

Builds a full dashboard (Sales by Category, Order Trends, Customer Loyalty, etc.)

🧱 Architecture Overview
Raw Data (CSV + JSON)
       ↓
Bronze Layer
       ↓
Silver Layer (cleaned, validated, typed)
       ↓
Gold Layer (aggregated KPIs)
       ↓
Dashboard (Databricks)

📂 Project Structure
/
├── notebooks/
│   ├── bronze_ingestion.py
│   ├── silver_cleaning_transformation.py
│   └── gold_aggregation.py
│
├── data_sample/
│   ├── orders.csv
│   └── customers.json
│
├── dashboard/
│   ├── retail_dashboard_overview.png
│   ├── sales_by_category.png
│   ├── order_trends.png
│   └── loyalty_distribution.png
│
├── README.md
└── LICENSE

🥉 Bronze Layer — Raw Ingestion

The raw data contains:

orders.csv

order_id

order_date (multiple date formats)

customer_id

product_id

product_name

category

quantity

price

payment_type

order_status

customers.json

customer_id

customer_name

city

loyalty_level

Data is loaded into Bronze as-is for traceability.

🥈 Silver Layer — Cleaning & Transformation (PySpark)

Major cleaning steps performed:

✔ Handle multiple date formats using coalesce()
order_date = coalesce(
    to_timestamp(trim(col("order_date")), "dd/MM/yyyy"),
    to_timestamp(trim(col("order_date")), "MM/dd/yyyy"),
    to_timestamp(trim(col("order_date")), "yyyy-MM-dd"),
    to_timestamp(trim(col("order_date")), "dd-MM-yyyy"),
    to_timestamp(trim(col("order_date")), "yyyy/MM/dd"),
)

✔ Remove spaces, convert strings to lowercase
✔ Cast columns to correct types
✔ Handle null or blank quantity
✔ Remove invalid characters from price
✔ Join CSV + JSON to create enriched dataset
🥇 Gold Layer — Business Aggregations

Final tables created:

📌 Total Sales per Category
📌 Order Trends Over Time
📌 Customer Loyalty Distribution
📌 Returned Amount by City
📌 Average Order Value (AOV)

Formula:

AOV = Total Sales / Number of Orders

📌 Average Price per Item

Formula:

Avg Price per Item = Total Revenue / Total Quantity Sold


These aggregates feed directly into the dashboard.

📊 Dashboard (Databricks)

Below are some sample dashboard components:

Total Sales by Category

Order Trends Over Time

Returned Amount by City

Customer Loyalty Pie Chart

KPI Cards

Average Order Value

Average Price per Item

(Screenshots included inside the /dashboard folder.)

🚀 How to Run This Project
1. Import the notebooks into Databricks

Menu → Workspace → Import

2. Upload sample CSV & JSON

Go to Data → Add Data

3. Run the workflow in order

Bronze

Silver

Gold

Dashboard queries

4. Visualize results using Databricks Dashboards
📦 Technologies Used

Databricks (Free Edition)

PySpark / Spark SQL

Delta Tables

CSV + JSON sources

Databricks Dashboarding

🙌 Author

Roshan Fareed
Email: roshanfareed53@gmail.com

📝 License

MIT License
