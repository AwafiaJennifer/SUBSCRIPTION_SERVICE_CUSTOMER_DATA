# About Dataset

## Subscription Service Company’s Customer Data Analysis

This is my second project, given to me by **The Incubator Hub**.

# Introduction

This section provides an analysis of customer data from a subscription service, aimed at understanding customer behavior, demographics, and purchasing patterns. Using SQL, Excel, and Power BI, the project segments customers based on key metrics and identifies high-value subscribers.

## Objectives

- Understand subscriber demographics and purchasing behavior.
- Identify high-value subscribers and frequent purchasers.
- Segment subscribers based on buying patterns and preferences.

## Data Sources

- **Subscriber Profiles**: Contains data on subscriber demographics such as location and subscription amount.
- **Subscription Transaction History**: A record of each subscriber’s purchases, including product details, transaction dates, and purchase amounts.

## Analysis Process

### Excel

1. **Data Cleaning**: 
   - Missing values and duplicates were handled in Excel.

2. **Exploration**: Conducted exploratory analysis to understand the data structure and identify any patterns or anomalies. Key metrics included:
   - Revenue
   - Average sales per product
   - Total revenue by region
   - Grand total revenue
   - Total number of products
   - Total revenue per product
   - Total quantity per product sold

3. **Pivot Tables**: Created pivot tables for insights into sales by product, region, and month.

4. **Metrics Calculation**: Calculated average sales per product and total revenue by region to gauge sales performance.

   ![Screenshot (5)](https://github.com/user-attachments/assets/68d7f2da-7d3a-45a4-a29c-bfa87c868297)
   ![Screenshot (10)](https://github.com/user-attachments/assets/98b04910-78f8-4d31-8eb9-51aa4abd5fe7)

### SQL

**Data Aggregation**:
- SQL was used to aggregate subscriber data and calculate metrics like total purchase amount, average transaction value, and purchase frequency.

**Segmentation**:
- Subscribers were segmented based on frequency, recency, and monetary value using RFM (Recency, Frequency, Monetary) analysis.

**Querying**:
- Example queries include:

   ```sql
   -- Total number of customers from each region
   SELECT 
       region,
       COUNT("customerID") AS total_customers
   FROM 
       customer_data 
   GROUP BY 
       region
   ORDER BY 
       total_customers DESC;

   -- Most popular subscription type by number of customers
   SELECT 
       "subscriptionType",
       COUNT("customerID") AS customer_count
   FROM 
       customer_data
   GROUP BY 
       "subscriptionType"
   ORDER BY 
       customer_count DESC
   LIMIT 1;

   -- Customers who cancelled their subscription within 6 months
   SELECT 
       "customerID",
       "customer_name",
       "region",
       "subscriptionType",
       "subscriptionStart",
       "subscriptionEnds"
   FROM 
       customer_data
   WHERE 
       cancelled = 'TRUE'
       AND "subscriptionEnds" <= "subscriptionStart" + INTERVAL '6 months';

   -- Calculate average subscription duration for all customers
   SELECT 
       AVG(
           "subscriptionEnds" - "subscriptionStart"
       ) AS avg_subscription_duration_days
   FROM 
       customer_data;

   -- Customers with subscription longer than 12 months	
   SELECT 
       "customerID",
       "customer_name",
       "region",
       "subscriptionType"
   FROM 
       customer_data
   WHERE 
       AGE("subscriptionEnds", "subscriptionStart") > INTERVAL '12 months'
   ORDER BY 
       "customer_name" ASC
   LIMIT 1;

   -- Total revenue by subscription type
   SELECT 
       "subscriptionType",
       SUM("revenue") AS total_revenue
   FROM 
       customer_data 
   GROUP BY 
       "subscriptionType"
   ORDER BY 
       total_revenue DESC;

   -- Top 3 regions by subscription cancellations
   SELECT 
       region,
       COUNT("customerID") AS cancellations
   FROM 
       customer_data
   WHERE 
       cancelled = 'TRUE'
   GROUP BY 
       region
   ORDER BY 
       cancellations DESC
   LIMIT 3;

   -- Total number of active and cancelled subscriptions
   SELECT 
       COUNT(
           CASE WHEN cancelled = 'FALSE' THEN 1 END
       ) AS active_subscriptions,
       COUNT(
           CASE WHEN cancelled = 'TRUE' THEN 1 END
       ) AS cancelled_subscriptions
   FROM 
       customer_data;

   ### Power BI

Power BI was used to create a series of interactive dashboards, providing visual insights into customer and subscription data:

- **Subscriber Demographics**: Visualized demographic information of subscribers, including regional distributions and age groups, enabling a clearer understanding of the customer base.

- **Subscription Purchase Behavior**: Analyzed subscription purchases over time, showcasing trends in popular subscription types and purchase frequency.

- **Sales Trends for the Year**: Illustrated monthly and quarterly sales trends, identifying peak periods and seasonal fluctuations to help with sales forecasting.

- **Regional Purchasing Trends**: Displayed data on purchasing behaviors by region, revealing high-revenue areas and growth opportunities.

   ![Screenshot (27)](https://github.com/user-attachments/assets/badb1df4-111d-4e3d-ad5d-30bdb3770f13)
   ![Screenshot (28)](https://github.com/user-attachments/assets/8be16c77-b7d6-43b5-9e80-03394f42dcfa)


  ## Key Insights

- **High-Value Subscribers**: Identified subscribers with the highest purchase frequency and transaction values, pinpointing key customer segments for potential loyalty programs.
- **Subscriber Preferences**: Analyzed popular products and categories based on subscription purchases, helping inform product and marketing strategies.
- **Regional Insights**: Observed regional trends in subscriber purchases, providing insight into geographic areas with the highest revenue and growth potential.

## Key Features

- **SQL Queries**: Used for detailed segmentation and analysis, including RFM (Recency, Frequency, Monetary) scoring and demographic breakdowns.
- **Excel Analysis**: Created Pivot Tables for in-depth insights into sales performance by product, region, and month.
- **Power BI Dashboards**: Developed interactive visualizations to explore data trends, customer segments, and revenue sources.
- **Actionable Insights**: Produced targeted recommendations for marketing strategies, personalized promotions, and product positioning for high-value subscribers.

   
Each dashboard allows stakeholders to interact with the data, offering valuable insights into key metrics like revenue, customer demographics, and regional sales performance.



