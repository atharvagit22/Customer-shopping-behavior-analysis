# Customer Shopping Behavior & Consumer Trends Analytics

End-to-end analysis of 3,900 retail transactions using **Python, SQL (SQLite) and Power BI** to understand what drives customer spending, satisfaction and loyalty.

## Business Problem

A retail company wants to understand shopping behavior across demographics, product categories and channels in order to improve sales, customer satisfaction and long-term loyalty. The analysis focuses on how discounts, reviews, seasons and payment preferences influence purchase decisions and repeat purchases.

> **Key question:** How can the company leverage consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?

## Dataset

3,900 rows and 16 columns.

| Group | Columns |
|---|---|
| Demographics & Location | Customer ID, Age, Gender, Location |
| Product & Purchase | Item Purchased, Category, Purchase Amount (USD), Size, Color, Season |
| Experience & Engagement | Review Rating, Subscription Status, Discount Applied, Previous Purchases, Payment Method, Frequency of Purchases |

## Approach

1. **Data preparation (Pandas):** schema and quality checks, duplicate handling, missing-value imputation (review rating filled with the category median and flagged), and validation with assertions.
2. **Feature engineering:** age groups, spend tiers (quartiles), loyalty segments, repeat-customer flag, numeric purchase frequency (days) and rating bands.
3. **SQL analysis (SQLite):** the cleaned data is loaded into an in-memory database and analysed with `GROUP BY`, `HAVING`, CTEs, window functions (`ROW_NUMBER`, `NTILE`, `SUM() OVER`), conditional aggregation and joins, plus indexes verified with `EXPLAIN QUERY PLAN`.
4. **Visualization (Matplotlib / Seaborn):** eight charts covering category and season performance, discount impact, demographics vs spend, ratings, loyalty, payments and geography.
5. **Power BI blueprint:** star-schema data model, DAX measures and a three-page dashboard layout.
6. **Executive summary:** key findings, recommendations and limitations generated from the data.

## Analyses Included

- Revenue and revenue share by category, plus top three items per category
- Seasonal revenue patterns by category
- Discounted vs non-discounted spend, with a confidence interval on the difference
- Spend by age group and gender
- Review rating distribution and category-level satisfaction
- Subscriber vs non-subscriber spend and repeat-purchase rate
- Payment method and purchase frequency patterns
- High-value customer segmentation (high spend and high loyalty) using a SQL join
- Top locations by revenue
- Correlation analysis of numeric drivers

## Visuals

| | |
|---|---|
| ![Sales by category and season](figures/01_sales_by_category_season.png) | ![Discount impact](figures/02_discount_impact.png) |
| ![Demographics vs spend](figures/03_demographics_vs_spend.png) | ![Review ratings](figures/04_review_ratings.png) |
| ![Loyalty and subscription](figures/05_loyalty_subscription.png) | ![Payment and frequency](figures/06_payment_frequency.png) |

## Power BI Dashboard

The notebook (Section 4) documents the full dashboard design:

- **Data model:** star schema with `Fact_Shopping` and dimension tables for customer, category, season and payment method.
- **DAX measures:** Total Revenue, Average Order Value, Unique Customers, Repeat Purchase Rate, Discount Usage %, Discount AOV Lift, Revenue Share % and Category Revenue Rank.
- **Pages:** Executive Overview, Customer Behavior & Loyalty, Product & Experience.

## Repository Structure

```
.
├── Customer_Shopping_Behavior_Analytics.ipynb   # full analysis notebook
├── shopping_behavior.csv                        # raw dataset
├── cleaned_shopping_data.csv                    # cleaned and feature-engineered data (Power BI input)
├── shopping.db                                  # SQLite database
├── figures/                                     # exported charts
├── requirements.txt
└── README.md
```

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the notebook
jupyter notebook Customer_Shopping_Behavior_Analytics.ipynb
```

Run all cells from top to bottom. The notebook reads `shopping_behavior.csv` from the same folder (configurable through `DATA_PATH`).

## Tech Stack

Python (Pandas, NumPy, Matplotlib, Seaborn), SQL (SQLite), Power BI (DAX), Jupyter Notebook.

## Limitations

- The data has no order dates, so season is used as a proxy for time and time-series trends cannot be measured.
- Findings are associations, not causal effects.
- Repeat purchasing is inferred from `Previous Purchases` using an adjustable threshold.
- No margin or cost data is available, so the effect of discounts on profit is not measured.

## Possible Next Steps

- Add order dates, margin, returns and sales channel to the data
- Customer segmentation with RFM and K-Means clustering
- Predictive model for repeat purchase or subscription
- A/B test of the discount strategy

## Author

**Atharva Lambde**
📧 atharvalambde@gmail.com ·  [GitHub](https://github.com/atharvagit22)
 If you found this project useful, please star the repository.
