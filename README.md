# ⚡ Electricity Demand Forecasting with SARIMAX, Prophet, and XGBoost

## 📖 Overview
This repository contains my MSc dissertation project on **medium-term electricity demand forecasting** in the UK.  
The study compares the following key modelling approaches:

- **SARIMA** Trained on past historical data
- **SARIMAX Baseline and Hyper Tuned** (classical statistical time-series with exogenous variables)  
- **Prophet Baseline and Hyper Tuned** (Meta’s additive time-series forecasting model)  
- **XGBoost Basedline and Tuned** (tree-based gradient boosting for regression)

The models are trained and evaluated using **historical demand** and **weather data of four major cities of the UK**, along with I also incorporate the **bank_holiday** effect, as during these days demand is lower, to assess accuracy in capturing daily, weekly, and seasonal trends.

---

## 📂 Contents
The key files are:

- `demanddata2021.csv, demanddata2022.csv, demanddata2023.csv, demanddata2024.csv ` → These files contain the data about the electricity demand in the UK for past four year.
- `23087309.ipynb` → Main Jupyter Notebook (data prep, models, evaluation)  
- `uk_weather_data_2021_2024.csv` → This contains the weather data of four major cities of the UK 

---

## 🌍 Data Sources
- **Electricity Demand Data**: NESO [NESO Energy](https://www.neso.energy/) 
- **Weather Data**: [Open-Meteo API](https://open-meteo.com/).  
- **Banking Holidays Data**
⚠️ **Note on Weather Data**:  Fetched from [GOV](https://www.gov.uk/bank-holidays)
The Open-Meteo API sometimes blocks repeated requests from the same IP address when fetching large amounts of historical weather data.  
To ensure reproducibility:  
- The API fetch code is included but **commented out** in the notebook.  
- Instead, a **pre-fetched CSV** (`uk_weather_data_2021_2024.csv`) is used for training and evaluation.

---
### ⚙️ Data Preprocessing Steps

1. **Standardize Date Formats**  
   - The NESO dataset contained four years of data in separate CSV files, each with different date formats.  
   - The first step was to **standardize the date column** across all files and then combine them into a single dataset.  

2. **Convert to Hourly Resolution**  
   - The raw data was recorded in **settlement periods** (half-hourly).  
   - To aggregate into an hourly basis, features such as **demand, generation, and imports** were summed for every two consecutive settlement periods.  

3. **Create Timestamp Column**  
   - A new **timestamp column** was generated, starting from 12:00 A.M., aligned with settlement periods in the National Grid data.  

4. **Merge with Weather Data**  
   - Finally, the processed grid demand data was **merged with temperature data** using the **nearest timestamp matching** method.
  
---
### 🔧 Feature Engineering

- **Lag Features**  
  - Created lagged demand variables (e.g., previous day’s demand, previous week’s average demand) to capture temporal dependencies.  

- **Rolling Statistics**  
  - Computed rolling mean (7-day moving average) and rolling standard deviation to model short-term fluctuations in demand.  

- **Calendar Features**  
  - Extracted **month, weekday, weekend indicator, bank holidays** to capture seasonality and human behavior patterns.  

- **Exogenous Variables**  
  - Added weather-related regressors such as **temperature** and **wind speed**, which strongly influence energy consumption.  


---

### 🤖 Model Training & Evaluation

- **SARIMAX**  
  - Captured temporal dependencies with **autoregressive and moving average components**.  
  - Exogenous features (temperature, calendar events, lag demand) were included for improved accuracy.  

- **Prophet**  
  - Used for trend and seasonality modeling (weekly & yearly cycles).  
  - Incorporated external regressors (temperature, weekend, holiday, lag demand).  

- **XGBoost**  
  - Applied gradient boosting with engineered features.  
  - Hyperparameters tuned using **time series cross-validation** to prevent overfitting.  

- **Evaluation Metrics**  
  - Models were compared using **RMSE, MAE, and MAPE** to assess prediction performance.
---

To access this 
### Clone repository
git clone [link](https://github.com/Akmal1995/fyp.git)

cd <23087309.ipynb>

### Install dependencies
pip install -r requirements.txt

# Open the notebook
jupyter notebook notebooks/23087309.ipynb


