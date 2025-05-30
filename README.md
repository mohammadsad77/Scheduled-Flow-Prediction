# Scheduled-Flow-Prediction-ML-
Scheduled Flow Prediction Between Ireland and Great Britain Project Overview This project aims to predict the scheduled electricity flow (scheduled_flow) between Ireland and Great Britain, measured in megawatts (MW), using historical data and machine learning models. The flow is influenced by economic factors (e.g., day-ahead price differences) and temporal patterns (e.g., hour of day, day of week, season). Accurate predictions can optimize energy distribution, reduce costs, and ensure grid stability for energy providers. The project includes: Exploratory Data Analysis (EDA) to identify patterns and relationships.

Feature engineering to create predictive features.

Model training and evaluation using various algorithms (e.g., XGBoost, SVR, Random Forest).

Source Data is collected from the electricity market between Great Britain and Ireland.

It includes price and flow data at half-hourly intervals (48 periods per day).

The dataset is a time-series, where temporal order matters (e.g., Day 1 affects Day 2).

Columns sd_uk: Settlement date in Great Britain (e.g., 2023-01-01).

sp_uk: Settlement period (1 to 48, representing half-hours).

delivery_start_uk, delivery_end_uk: Delivery start/end times in UK local time.

delivery_start_utc, delivery_end_utc: Delivery start/end times in UTC.

gb_da_price: Day-ahead price in Great Britain (£/MWh, range: 50 to 200).

irl_da_price: Day-ahead price in Ireland (£/MWh, range: 40 to 180).

scheduled_flow: Scheduled electricity flow (MW, range: -1000 to +1000). Positive: Flow from Ireland to Great Britain.

Negative: Flow from Great Britain to Ireland.

Methodology

Preprocessing Time Format Conversion: Converted delivery_start_uk to datetime format. Enables extraction of temporal features (e.g., hour, day, month).
Remove Missing Values: Used data.dropna() to remove rows with NaN values caused by lagged features.

Data Standardization: Standardized features using StandardScaler to ensure equal scale.

Essential for models like SVR, which are sensitive to feature scales.

Feature Engineering Temporal Features: hour: Hour of the day (0-23).
day_of_week: Day of the week (0=Monday, 6=Sunday).

is_weekend: 1 for weekends (Saturday, Sunday), 0 for weekdays.

month: Month of the year (1-12).

Purpose: Capture cyclical patterns (e.g., higher demand during peak hours or weekdays).

Economic and Time-Series Features: price_diff: gb_da_price - irl_da_price.

price_diff_lag1, price_diff_lag2: Lagged price differences (1 and 2 periods back).

flow_lag1, flow_lag3: Lagged flows (1 and 3 periods back).

price_diff_roll_mean_7d, flow_trend_7d: 7-day rolling mean (336 half-hour periods).

price_diff_hour: Interaction between price difference and hour.

Purpose: Lagged features capture short-term dependencies (e.g., autocorrelation in flow).

Rolling means capture long-term trends.

Interaction features model non-linear relationships (e.g., price difference impact varies by hour).

Exploratory Data Analysis (EDA) EDA was performed to identify patterns and relationships in the data. Below is a detailed analysis of the 12 EDA charts.
Modeling Models Used: XGBoost
SVR (Support Vector Regression)

Random Forest

Stacking (meta-model: XGBoost)

Voting (weighted average of base models)

Evaluation Metrics: Mean Absolute Error (MAE)

R² Score

Feature Importance: Used SHAP (SHapley Additive exPlanations) to identify key features: flow_lag1: Highest importance (0.8).

price_diff: High importance (0.3).

price_diff_lag1, hour: Moderate importance (0.2, 0.1).# Scheduled-Flow-Prediction
