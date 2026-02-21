Customer Churn Prediction Analysis
📊 Overview
customer_churn_prediction.py is a comprehensive Python analysis script for telecom customer churn. Converted from a Google Colab notebook, it transforms raw customer data into executive-ready visualizations revealing:

Why customers churn (competitors = 33% of cases)

Revenue impact by customer traits

Customer segmentation (High/Low Value × Risk/Safe)

Retention priorities (focus on volume, not just whales)

Global Churn Rate: 26.6%
Key Insight: Month-to-Month contracts + competitor offers = biggest revenue threats

🚀 Quick Start
bash
# 1. Install dependencies
pip install pandas matplotlib seaborn numpy

# 2. Place telecom_customer_churn.csv in same folder
# 3. Run (best in Jupyter/Colab)
python customer_churn_prediction.py
5 charts auto-generated with zero configuration.

📋 Requirements
Package	Purpose
pandas	Data manipulation
matplotlib	Charts & figures
seaborn	Enhanced visuals
numpy	Math operations
Python 3.7+ required

🗄️ Data Requirements
File: telecom_customer_churn.csv (~7K rows)

Essential Columns:

text
Customer ID, Monthly Charge, Tenure in Months, Customer Status (Stayed/Churned/Joined)
Churn Reason, Contract, Offer, Internet Type, Online Security, Payment Method
Total Revenue, Total Refunds, Number of Referrals, Age
Download dataset: Search "telecom customer churn dataset Kaggle" or use Telco churn sample data.

📁 File Structure
text
customer_churn_prediction.py  # Main analysis (28K lines)
telecom_customer_churn.csv    # Dataset (REQUIRED)
README.md                    # This file
outputs/                     # Optional: save charts here
🎯 Core Analysis Flow
1. Data Cleaning (Lines 20-60)
text
- Fill missing services → "None"
- Standardize churn reasons  
- Categorize: Competitors/Support/Pricing/Product/Network/Other
2. Key Metrics (Lines 80-200)
text
NVF (Normalized Value Factor) = (Monthly Charge + Tenure + Referrals) / 3
• 0-1 scale, ≥0.6 = "High Value"

NCRF (Normalized Churn Risk Factor) = Service feature risk score
• 0-1 scale, ≥0.5 = "Low Risk"
3. Customer Segments
Value → Risk	High Value	Low Value
Safe	Strategic VIP	Mass Market
@ Risk	Priority 1	Volume Risk
Churned	Revenue Leak	Volume Loss
4. Generated Visualizations
text
1. Churn Reason Pie + Subcategory Bars
2. Revenue Hotspots (Top 15 traits by $ loss)
3. Feature Lift Analysis (50+ features vs 26.6% baseline)  
4. 4x4 Revenue Dashboard (accounts/$ by segment)
5. NVF vs NCRF Scatter Plot (customer distribution)
💡 Key Business Insights
text
🔥 #1 Revenue Risk: Month-to-Month contracts
🏆 Competitors cause 33% churn (devices + offers)
📈 81% revenue from Low Value customers → volume retention > whale hunting
⚠️  Service features neutral (No/Yes same churn rate)
💰 High Value Churn = $104 avg vs Low Value = $70 avg
⚙️ Customization Guide
Test Thresholds
python
# Default: NVF=0.6, Risk=0.5
df_test = simulate_thresholds(0.5, 0.4)  # More customers "At Risk"
print(df_test)
Add Features
python
risk_columns += ['NewFeature1', 'NewFeature2']
Color Theme
python
facecolor    = "#5f6f63"  # Dark background
churn        = "#f7f4d5"  # Yellow
stay         = "#d3969c"  # Pink
stayat       = "#fffbf0"  # Cream
📈 Example Outputs
Chart 1: Root Causes

text
Competitors: 11.9% → Better devices/offers
Customer Support: 5.9% → Attitude/expertise issues
Chart 2: Revenue Hotspots

text
1. Contract: Month-to-Month  → $12.3M cumulative loss
2. Online Security: No      → $8.7M  
3. Fiber Optic internet    → $7.2M
🔧 Troubleshooting
Error	Fix
FileNotFoundError	Download telecom_customer_churn.csv
No plots showing	Use Jupyter/Colab (%matplotlib inline)
KeyError: 'ColumnX'	Verify CSV has exact column names
Slow execution	Normal (~7K rows, 10-30s runtime)
🛠️ Technical Notes
Designed for Jupyter/Colab - plots display inline

Hard-coded column names - modify pd.read_csv() for custom data

Colors optimized for dark theme

No ML model - pure exploratory analysis + segmentation

🚀 Usage Examples
bash
# Standard run
python customer_churn_prediction.py

# In Jupyter (recommended)
%run customer_churn_prediction.py

# Test thresholds interactively
v_test = simulate_thresholds(0.55, 0.45)
v_test
📊 Sample KPI Output
text
High Value / Stayed @ Risk: 1,231 accounts, $108K monthly value (18.7%)
Low Value  / Churned:       523K accounts, $48K monthly value (42.4%)
📄 License
MIT License - Free for commercial/personal use. No warranty.

text
Copyright (c) 2026 Poorani M (Bengaluru, India)
🎉 Next Steps
Run analysis → Get instant retention roadmap

Adjust thresholds → Find optimal segmentation

Export insights → plt.savefig('churn_dashboard.png')

Build model → Use segments as features for ML churn prediction

💎 Value Proposition: Raw CSV → Executive dashboard in 30 seconds. Perfect for stakeholder presentations, retention strategy, or data science portfolio projects.

Made in Bengaluru 🇮🇳 by Poorani M - Feb 2026
