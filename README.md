# EV_Vehicle_Charge_Demand
Overview
This project analyzes electric vehicle (EV) adoption trends across different counties in the United States. The dataset contains information about EV populations, including battery electric vehicles (BEVs) and plug-in hybrid electric vehicles (PHEVs), along with traditional vehicle counts for comparison.

Objective
To predict energy demand (kWh) for EV charging stations using:
-Date and time features
-Weather data (e.g., temperature)
-Holiday/working day information

Key Steps Covered
1. Data Loading & Cleaning
Loaded a dataset with features like date, hour, temperature, holiday, etc.

Handled missing values and cleaned the time-series format.

2. Feature Engineering
Created new features:

is_weekend

day_of_week

month

hour bucketed as time_of_day

Converted categorical data (like holidays) into numerical formats.

3. Exploratory Data Analysis (EDA)
Visualized charging trends across:

Time (hour/day/month)

Temperature

Holiday vs. non-holiday

Used plots to uncover demand patterns.

4. Model Building
Multiple regression models were trained and tested:

Linear Regression

Decision Tree Regressor

Random Forest Regressor

Gradient Boosting Regressor

XGBoost Regressor

Each model was evaluated using:

R² Score

MAE (Mean Absolute Error)

RMSE (Root Mean Squared Error)

5. Results & Visualization
Displayed feature importance from tree-based models.

Plotted actual vs. predicted demand.

Choose the best-performing model based on metrics.
