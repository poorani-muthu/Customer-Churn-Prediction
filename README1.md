This Python script analyzes telecom customer data to predict and visualize churn (customers leaving the service). <br>It loads data, cleans it, calculates customer value and risk scores, and creates detailed charts to show churn patterns.
<br>
## Imports and Setup<br>
The code starts by importing key libraries. Pandas (`pd`) handles data like Excel spreadsheets in tables called DataFrames. <br>Matplotlib (`plt`) and Seaborn (`sns`) create charts, while NumPy (`np`) does math operations. These are standard tools for data analysis in Python. 
<br>
It loads customer data from "telecom_customer_churn.csv" into `df`, a table with columns like 'Customer ID', 'Monthly Charge', 'Customer Status' (Stayed/Churned), and service details.
<br>
## Data Cleaning<br>
Missing values in service columns (like 'Offer', 'Internet Type') get filled with 'None'. Churn reasons are standardized, e.g., <br>"Lack of affordable download/upload speed" becomes "Lack of affordable speed". 
<br>
A function `map_churn_category` groups churn reasons into buckets: Competitors, Customer Support, Pricing, Product, Network, or Other. <br>It applies this to create a new 'Churn_Category' column.
<br>
## Core Analysis Preparation
<br>- Filters data to `analysis_df` (only Stayed/Churned customers, excluding new "Joined").
<br>- Creates `norm_df` for Normalized Value Factor (NVF): Scales 'Monthly Charge', 'Tenure in Months', and 'Number of Referrals' to 0-1 range using `min_max_scale`. <br>Averages them for NVF (Y-axis: higher = more valuable customer). 
<br>- Computes Normalized Churn Risk Factor (NCRF): For risk features (Contract, Online Security, etc.), calculates how much each option increases churn vs. average. <br>Sums raw scores, normalizes to 0-1 (higher NCRF = lower risk, X-axis). 
<br>-Merges into `master_df` with segments: Value_Tier (High/Low based on NVF >=0.6), Strategic_Segment (Stayed @ Risk, Stayed Safe, Churned based on NCRF).<br>
## Threshold Simulation<br>
`simulate_thresholds(v_threshold, r_threshold)` tests different cutoffs. It copies data, reclassifies tiers, merges charges, and groups to show accounts, average charge, total value, and % within tiers. <br>Example calls test thresholds like 0.5 or 0.6.<br>
## Churn Reason Visuals <br>
Defines colors (e.g., `churn="#f7f4d5"`) and `churn_subcategory_distribution` for % breakdowns. `plot_churn_subcategory` makes horizontal bar charts. A complex figure (3x4 grid) shows a pie chart of categories <br>(Competitors biggest at ~12%) with arrows to subcategory bars, titled "Churn Is Not Evenly Distributed".<br>
## Additional Features and Prep <br>
Merges scores back to full `prepared` DataFrame, fills new customers as 'Joined'/'Acquisition Tier'. Adds Age_Group (Gen Z to Senior) and Revenue_Tier (Entry to VIP based on Total Revenue). <br>
## Revenue Impact Charts 
<br>-"Churn Hotspots" bar chart: Top traits in churned customers by count and cumulative revenue loss (e.g., Month-to-Month contract highest exposure). 
<br>- "Feature-Level Churn Intelligence": Three-panel plot with Lift % (relative churn risk vs. average), feature names, and churn probability bars. 
<br>- 4x4 grid dashboard: Boxes show revenue/accounts per segment (e.g., High Value Churned: $320k), plus scatter plot of NVF vs. NCRF colored by segment, emphasizing volume over elite retention.<br>
## Purpose <br>
This turns raw data into business insights: Competitors drive most churn, focus retention on at-risk high-volume customers, not just whales. Run in Jupyter/Colab; needs the CSV file. 
