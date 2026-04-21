# EV_Vehicle_Charge_Demand

[![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-Dashboard-ff4b4b.svg)](https://streamlit.io/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange.svg)](https://scikit-learn.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Overview

**EV_Vehicle_Charge_Demand** is a machine learning-powered Streamlit application that forecasts electric vehicle adoption trends at the county level across the United States.

As EV adoption grows, planners, utility providers, charging infrastructure companies, and local governments need better visibility into where demand may rise next. This project addresses that problem by using historical county-level EV population data to forecast cumulative EV adoption for the next **36 months**.

The application allows users to select a county, view historical EV adoption, generate a 3-year forecast, and compare adoption trends across up to three counties through interactive visualizations.

## Features

- Forecasts county-level EV adoption for the next **3 years**
- Uses a trained **Random Forest Regressor** for time-aware EV demand prediction
- Supports county selection from **269 processed U.S. counties**
- Compares EV adoption trends across up to **3 counties**
- Visualizes historical and forecasted cumulative EV growth
- Uses lag features, rolling averages, percentage change, and growth slope for forecasting
- Includes a Streamlit dashboard for simple local execution and presentation
- Ships with the trained model artifact and preprocessed dataset

## Architecture / How It Works

The project follows a simple machine learning pipeline:

1. **Raw Data Ingestion**
   - Loads county-level EV population data from `Electric_Vehicle_Population_By_County.csv`.

2. **Data Cleaning & Preprocessing**
   - Converts date fields into datetime format.
   - Handles missing county and state values.
   - Sorts records by county and date.
   - Encodes counties using label encoding.

3. **Feature Engineering**
   - Creates time-based features such as year, month, numeric date, and months since start.
   - Builds lag features from previous EV totals.
   - Computes rolling 3-month average EV totals.
   - Calculates 1-period and 3-period percentage changes.
   - Computes cumulative EV growth slope using a 6-month rolling window.

4. **Model Training**
   - Trains a `RandomForestRegressor`.
   - Uses `RandomizedSearchCV` for hyperparameter tuning.
   - Uses a chronological train/test split with `shuffle=False`.

5. **Forecasting**
   - Loads the trained model from `forecasting_ev_model.pkl`.
   - Generates recursive monthly predictions for a 36-month horizon.
   - Updates lag, rolling, percentage-change, and growth-slope features after each forecast step.

6. **Dashboard**
   - Streamlit provides county selection, comparison views, cumulative charts, and growth summaries.

## Tech Stack

**Machine Learning / AI**

- scikit-learn
- RandomForestRegressor
- RandomizedSearchCV
- Joblib model serialization

**Backend / APIs**

- Python
- Streamlit

**Cloud / Deployment**

- Local Streamlit app
- Cloud deployment not configured yet
- Suitable for Streamlit Community Cloud, Render, or Hugging Face Spaces

**Tools / Libraries**

- Pandas
- NumPy
- Matplotlib
- Jupyter Notebook

## Performance & Metrics

**Model Performance**

- MAE: `0.01`
- RMSE: `0.06`
- R2 Score: `1.00`
- Best model: `RandomForestRegressor`
- Best parameters:
  - `n_estimators`: `200`
  - `max_depth`: `15`
  - `min_samples_split`: `4`
  - `min_samples_leaf`: `1`
  - `max_features`: `None`

**Dataset Size**

- Raw dataset: `20,819` rows
- Processed dataset: `12,573` rows
- Processed counties: `269`
- States/regions represented: `51`
- Date range: `2017-02-28` to `2024-02-29`

**Latency / Response Time**

- Local forecast generation: under `1 second` for a selected county *(approx)*
- Multi-county comparison: under `3 seconds` for up to 3 counties *(approx)*

**Improvements / Optimizations**

- Uses cached data loading through Streamlit.
- Stores a pre-trained model artifact to avoid retraining during app startup.
- Uses engineered temporal features to capture short-term adoption momentum.
- Recursively updates forecast features for each future month.

## Getting Started

### Prerequisites

- Python 3.10 or higher
- pip
- Git

### Installation

Clone the repository:

```bash
git clone https://github.com/SaiSugeet/EV_Vehicle_Charge_Demand.git
cd EV_Vehicle_Charge_Demand
```

Create and activate a virtual environment:

```bash
python -m venv .venv
```

On Windows:

```bash
.venv\Scripts\activate
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

### Run the Project

Start the Streamlit app:

```bash
streamlit run app.py
```

Then open the local Streamlit URL shown in the terminal, usually:

```text
http://localhost:8501
```

## Deployment

The project is currently configured for local execution. A cloud deployment can be added later using one of the following platforms:

- Streamlit Community Cloud
- Render
- Hugging Face Spaces
- Railway

For Streamlit Community Cloud, the deployment entry point should be:

```text
app.py
```

Required runtime files:

- `app.py`
- `requirements.txt`
- `preprocessed_ev_data.csv`
- `forecasting_ev_model.pkl`
- `ev-car.jpg`

## Project Structure

```text
EV_Vehicle_Charge_Demand/
|-- README.md
|-- LICENSE
|-- .gitignore
|-- app.py
|-- EV.ipynb
|-- requirements.txt
|-- Electric_Vehicle_Population_By_County.csv
|-- preprocessed_ev_data.csv
|-- forecasting_ev_model.pkl
`-- ev-car.jpg
```

**Key files**

- `app.py` - Streamlit dashboard for EV adoption forecasting and county comparison.
- `EV.ipynb` - Notebook containing preprocessing, feature engineering, model training, evaluation, and model export.
- `Electric_Vehicle_Population_By_County.csv` - Raw county-level EV population dataset.
- `preprocessed_ev_data.csv` - Cleaned and feature-engineered dataset used by the app.
- `forecasting_ev_model.pkl` - Trained Random Forest forecasting model.
- `requirements.txt` - Python dependencies required to run the project.
- `ev-car.jpg` - Dashboard image asset.

## Use Cases

- EV charging infrastructure planning
- County-level EV adoption forecasting
- Utility demand planning and grid-readiness analysis
- Data science portfolio demonstration
- Public policy and transportation trend analysis
- Comparing regional EV adoption growth patterns

## Future Improvements

- Deploy the app publicly using Streamlit Community Cloud or Render
- Add interactive charts with Plotly
- Add downloadable forecast reports
- Include charger availability and energy demand datasets
- Add state-level and national-level forecasting views
- Improve model validation with walk-forward time-series evaluation
- Add confidence intervals for forecast uncertainty
- Add automated model retraining pipeline
- Add screenshots and demo GIFs after deployment

## Contributing

Contributions are welcome. To contribute:

1. Fork the repository.
2. Create a new feature branch.
3. Make your changes.
4. Submit a pull request with a clear description.

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.
