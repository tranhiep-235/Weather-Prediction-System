🌤️ Weather Prediction System (HCMC) — Python & Machine Learning
Forecasting next-day temperature and rainfall category in Ho Chi Minh City using historical meteorological data and Random Forest models.

📌 Overview
This project builds two machine learning models to forecast weather in Ho Chi Minh City for the next day:
Temperature Forecasting (Regression) — predicts next-day average temperature (°C).
Rainfall Classification (Classification) — predicts next-day rainfall category (6 classes, based on WMO standards).
Data spans 11 years (2015–2026), collected via the Open-Meteo Historical Weather API, covering temperature, precipitation, wind, solar radiation, and evapotranspiration.

📊 Data
Source: Open-Meteo Archive API (ECMWF ERA5 reanalysis dataset)
Location: Ho Chi Minh City (10.8231°N, 106.6297°E)
Period: 2015-01-01 to 2026-01-10 (4,028 daily records)
Variables: mean/max/min temperature, precipitation, wind speed & direction, solar radiation, evapotranspiration

🔧 Feature Engineering
Lag features: temperature and rainfall from the previous 1–3 days (autoregressive signal)
Rolling features: 7-day and 30-day moving averages (trend smoothing)
Cyclic encoding: month represented as sin/cos to preserve seasonal continuity (Dec ↔ Jan)
Rainfall categories (WMO standard): No rain, Light, Moderate (6–15mm), Heavy (16–50mm), Very heavy (51–100mm), Extreme (>100mm)

Final feature set: 15 variables, ~4,000 samples after cleaning (dropped rows with missing lag/rolling/target values).

🤖 Models
Task	Model	Key Settings
Temperature (Regression)	RandomForestRegressor	n_estimators=150, random_state=42
Rainfall (Classification)	RandomForestClassifier	n_estimators=200, class_weight='balanced'
Train/test split: 80/20, chronological (no shuffle) to avoid data leakage and simulate real forecasting conditions.

📈 Results
Temperature Regression
MAE: 0.45°C
R²: 0.8381

Rainfall Classification
Overall accuracy: 53%
Per-class accuracy: No rain 73.7%, Light rain 52.5%, Moderate 48.6%, Heavy 8.8%
Class imbalance (majority "no rain" days) remains a challenge for rare/heavy-rain classes despite balanced class weighting.

🛠️ Tech Stack
Python, Pandas, NumPy
Scikit-learn (RandomForestRegressor, RandomForestClassifier)
Seaborn, Matplotlib (visualization)
Requests (API data collection)

🚀 How It Works
Fetch historical daily weather data from Open-Meteo API
Clean and engineer features (lag, rolling, cyclic month encoding)
Train Random Forest models on chronologically split data
Evaluate using MAE/R² (regression) and precision/recall/F1 + confusion matrix (classification)
Generate next-day forecast using the most recent observation

⚠️ Limitations & Future Work
Currently one-step-ahead (next-day only) forecasting
Does not account for large-scale climate drivers (El Niño, IOD)
Rare rainfall classes (heavy/extreme) underperform due to limited samples
Planned improvements: multi-step forecasting (3–7 days), LSTM/GRU models, ensemble methods (XGBoost, LightGBM), probabilistic forecasting, and multi-station spatial features

🎓 Academic Context
Developed as part of the Python for Data Science course, Faculty of Mathematics & Computer Science, Class 23TTH.
Team: Đoàn Anh Quân, Hà Tuấn Kiệt, Trần Tấn Hiệp, Lê Việt Hoàng Instructor: ThS. Hà Văn Thảo
