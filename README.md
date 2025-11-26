# Customer_Behavior_Analysis (SQL + Power BI + Python Project)
This project explores customer shopping behavior using Microsoft SQL Server, Power BI, and Python. It combines structured SQL queries, interactive visualizations, and robust data preprocessing to uncover insights into purchasing patterns, customer segmentation, product performance, and discount effectiveness.
The dataset contains 3,900 customer records with attributes such as age, gender, location, item purchased, category, purchase amount, review rating, subscription status, shipping type, and more. The goal is to extract actionable insights that support data-driven decision-making in marketing, sales, and operations.

# Project Objectives
- 🧠 Understand customer purchasing behavior across demographics and product categories
- 💰 Compare revenue and spending patterns across gender, age groups, and subscription status
- 🎯 Identify top-performing products and categories
- 🛍️ Evaluate the impact of discounts and shipping types on customer spend
- 🔁 Segment customers based on loyalty and purchase frequency
- 🧹 Clean and transform raw data for analysis
- 📊 Visualize trends using Power BI for executive-level reporting
- 📈 Provide strategic recommendations to improve customer engagement and profitabilit

#  Tools & Technologies
- Microsoft SQL Server (T-SQL)
- SQL Server Management Studio (SSMS)
- Power BI Desktop
- Python (pandas, pyodbc for database connectivity)
- Jupyter Notebook

# Python Data Exploration & Cleaning
Before analysis, the dataset was cleaned and transformed using Python:
  ### Data Loading & Inspection
- Loaded customer_shopping_behaviour.csv using pandas
- Verified structure with .info() and .describe(include='all')
- Identified 37 missing values in review_rating
  ### Missing Value Treatment
- Filled missing review_rating values using category-wise median imputation:
df['review_rating'] = df.groupby('category')['review_rating'].transform(lambda x: x.fillna(x.median()))

## Column Standardization
- Renamed columns to snake_case for consistency:
df.columns = df.columns.str.lower().str.replace(' ', '_')
df = df.rename(columns={'purchase_amount_(usd)': 'purchase_amount'})

## Feature Engineering
-- Created age_group using quantile-based binning:
labels = ['Young', 'Middle-aged', 'Adult', 'Old Age']
df['age_group'] = pd.qcut(df['age'], q=4, labels=labels)
-- Mapped frequency_of_purchases to numeric purchase_frequency_days:
frequency_mapping = {
    'Fortnightly': 14, 'Weekly': 7, 'Monthly': 30,
    'Quarterly': 90, 'Bi-weekly': 14, 'Annually': 365,
    'Every 3 Months': 90}
df['purchase_frequency_days'] = df['frequency_of_purchases'].map(frequency_mapping)

## Database Integration
- Connected to SQL Server using pyodbc
- Created and populated Customer_shopping_behaviour table in Test_DB
- Verified schema and inserted cleaned data row-by-row

# SQL Analysis Highlights
### Gender-Based Revenue
  - Calculate total revenue from male vs. female customers.
### High-Spending Discount Users 
 - Identify customers who used discounts and still spent above the average purchase amount.
### Top-Rated Products
- Retrieve the top products with the highest average review ratings.
### Shipping Type Impact
 - Compare average purchase amounts between Standard and Express shipping.
### Subscriber vs Non-Subscriber Behavior -
 - Compare average spend and total revenue between subscribed and unsubscribed customers.
### Discount Performance
 - Identify:
      Top 5 products most often purchased with discounts
      Products with the highest percentage of discounted purchases
### Customer Segmentation
 - Group customers into:
    New
    Returning
    Loyal
    based on previous purchases.
### Category-Level Product Ranking
 - Find the top 3 most purchased products within each category.
### Repeat Buyer Subscription Trend
 - Analyze whether customers with >5 previous purchases are more likely to subscribe.
### Revenue by Age Group
 - Generate total revenue by age group.
### Top Products by Age Group and Category
 - Retrieve the top purchased items per category per age group.

# Power BI Dashboard Insights
Your Power BI dashboard brings the data to life with interactive visuals and filters:
  ## Key Metrics
- Total Sales: $233K
- Average Sales: $60
- Number of Customers: 3.9K
- Average Rating: 3.8
  ## Sales by Category
- Clothing: $104.3K
- Accessories: $74.2K
- Footwear: $36.1K
- Outerwear: $18.5K
  ## Top-Selling Items
- Blouse, Shirt, Dress, Pants, Jewelry, Sunglasses, Belt, Scarf
  ## Sales by Age Group
- Young: $62.1K
- Adult: $59.2K
- Middle-aged: $56.0K
- Old Age: $55.8K
  ## Sales by Season
- Fall and Spring lead in seasonal sales
  ## Size & Gender Trends
- Size M dominates across both genders, with males spending more overall
  ## Discount & Subscription Stats
- 43% of purchases involved discounts
- 27% of customers are subscribers

# How to Use
- Open SQL Server Management Studio (SSMS)
- Create or select a database (e.g., Test_DB)
- Run the Python notebook to clean and upload data
- Execute queries from Customer_shopping_behaviour.sql
- Open the Power BI dashboard to explore visual insights

# Summary of Insights
- 👥 Male customers generate slightly more revenue, but female customers show strong engagement
- 🛍️ Discounts drive purchases, especially in accessories and clothing
- 🚚 Express shipping correlates with higher spend
- 🔁 Loyal customers are more likely to subscribe and spend more
- 🧓 Adults and middle-aged groups are the most profitable demographics
- 🛒 Blouses, shirts, and dresses are top performers across age groups

# Business Recommendations
- 🎯 Target loyal and repeat buyers with exclusive subscription benefits
- 📢 Promote high-rated products in campaigns
- 💸 Optimize discount strategies for high-converting items
- 🚀 Enhance express shipping for high-value customers
- 📬 Segment marketing by age group and category for tailored promotions
