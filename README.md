# ⚡ Electric Vehicle Population Forecasting

This project aims to forecast the future demand and growth of Electric Vehicles (EVs) using historical county-wise data. It utilizes machine learning techniques for modeling and provides a Flask-based web interface for easy deployment.

## 🚀 Project Overview

With the rise in EV adoption across regions, predicting future growth patterns becomes crucial for planning infrastructure like charging stations and grid loads. This project:

- Analyzes EV population data by U.S. counties
- Preprocesses and engineers features for modeling
- Trains a regression model to forecast EV count
- Provides a web application to serve predictions interactively

---

## 📊 Dataset

### `Electric_Vehicle_Population_By_County.csv`

- Source: Government EV registry (assumed)
- Contains fields like `County`, `City`, `Make`, `Model`, `Electric Range`, and `Vehicle Type`

### `preprocessed_ev_data.csv`

- Cleaned version of the dataset with relevant features selected and encoded
- Used for modeling and inference

---

## 🧠 Machine Learning Model

- Model: Likely a DecisionTreeRegressor or similar (saved as `forecasting_ev_model.pkl`)
- Input features: Processed variables derived from the raw dataset
- Output: Forecasted number of EVs in a given region

---

## 🖥️ Application

### `app.py`

A Flask web server that:

- Loads the trained model
- Accepts input data from users
- Returns the forecasted EV population



```bash
POST /predict
Payload: JSON with input features
Response: Forecasted EV count
