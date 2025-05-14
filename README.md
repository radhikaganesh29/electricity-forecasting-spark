# Electricity Load Forecasting with Apache Spark (PySpark + MLlib)

This machine learning project demonstrates how to use Apache Spark for large-scale time-series forecasting on a real-world electricity consumption dataset. We build a complete pipeline using PySpark and Spark MLlib to predict hourly electricity load in Germany.

---

## Dataset

- **Source**: [Open Power System Data – Time Series](https://data.open-power-system-data.org/time_series/)
- **Data**: Hourly electricity consumption and generation data from 2015 to 2020
- **Country Used**: Germany (DE_load_actual_entsoe_transparency)
- **Format**: CSV → Loaded into Databricks (Apache Spark)

---

## Apache Spark Workflow

**Steps**:
1. Uploaded CSV dataset to Databricks Community Edition
2. Loaded data into Spark DataFrame using PySpark
3. Performed time-series preprocessing:
   - Converted timestamp columns
   - Filtered and cleaned missing values
   - Engineered lag features:
     - lag_1h (1 hour ago)
     - lag_24h (1 day ago)
     - lag_168h (1 week ago)
4. Trained and evaluated three models using Spark MLlib:
   - Linear Regression (Baseline)
   - Random Forest Regressor
   - Gradient Boosted Trees (Best model)

---

## Lag Feature Logic

Lag-based predictors were engineered to help the model learn from historical trends:

| Feature   | Meaning                     |
|-----------|-----------------------------|
| lag_1h  | Load 1 hour before current  |
| lag_24h | Load 24 hours before        |
| lag_168h| Load 1 week before (168 hrs)|

These helped the model implicitly learn **daily and weekly seasonality**.

---

## Model Performance

| Model               | RMSE      |
|--------------------|-----------|
| Linear Regression  | 2144.07   |
| Random Forest      | 1547.61   |
| Gradient Boosted Trees (GBT) | **1535.80** |

The GBT model achieved the **lowest error** and best predictive performance.

---

## Visualizations

Visualizations were done using Pandas and Matplotlib:

1. **Raw Time Series Trends**  
   Hourly electricity load (2015–2020)
   
   ![IMG_1](https://github.com/user-attachments/assets/a629a4bc-a88d-414f-9570-165598b564f2)
   

3. **Zoomed Daily Trends**  
   Load patterns for January 2017 showing day/night cycles
   
   ![IMG_2](https://github.com/user-attachments/assets/537b552c-8a0c-4f81-ad61-9b64dae4d1a2)


5. **Predicted vs Actual** (Sample 100)  
   GBT model predictions vs actual values
   
   ![IMG_3](https://github.com/user-attachments/assets/ea35142c-12b6-43de-a912-e6eefdfd51fd)

---

## Key Insights

1. **Model Accuracy**
   - RMSE improved by ~28% from linear regression to GBT
   - Random Forest and GBT models captured nonlinear demand behavior better than linear

2. **Seasonality Captured**
   - Daily and weekly load cycles were effectively modeled using lag features
   - Forecasts closely track actual patterns during weekday and weekend transitions

3. **Scalable Pipeline**
   - Entire project was run using **Apache Spark on Databricks**
   - Demonstrates how to process large time-series data using Spark’s in-memory processing

---

