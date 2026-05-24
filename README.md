# PropPredict: Islamabad House Price Prediction System

An end-to-end machine learning system that scrapes Zameen.com, trains six regression models, and predicts house prices in Islamabad through a live interactive web dashboard.

<img width="2752" height="1536" alt="Islamabad_Property_Intelligence_System" src="https://github.com/user-attachments/assets/fca008a6-0288-44ec-99f8-811424156f16" />

---

## Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Data Preprocessing](#data-preprocessing)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Machine Learning Models](#machine-learning-models)
- [Model Evaluation](#model-evaluation)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [API Endpoints](#api-endpoints)
- [Contributors](#contributors)

---

## Project Overview

PropPredict is a complete house price prediction system built for Islamabad, Pakistan, developed as part of a Machine Learning project

The system covers the full data science pipeline — from raw web scraping through to a live Flask-powered prediction dashboard.

| Step | Description |
|------|-------------|
| Data Scraping | 300+ property listings scraped from Zameen.com using Selenium and BeautifulSoup |
| Preprocessing | Missing value handling, outlier capping at the 99th percentile, and label encoding |
| Model Training | Six regression algorithms trained and evaluated on an 80/20 split |
| Evaluation | MAE, MSE, RMSE, and R² scores computed consistently across all models |
| Web Dashboard | Flask-powered interactive prediction system with four tabs |

---

## Dataset

Property listings scraped from Zameen.com for Islamabad (2024).

| Feature | Description |
|---------|-------------|
| `price_pkr` | Property price in Pakistani Rupees (target variable) |
| `location` | Sector or area in Islamabad (e.g., DHA, E-11, F-7) |
| `bedrooms` | Number of bedrooms |
| `bathrooms` | Number of bathrooms |
| `size_sqft` | Total area in square feet |
| `property_type` | House, Flat, or Farm House |
| `built_year` | Year of construction |
| `parking_spaces` | Number of parking spaces |
| `servant_quarters` | Number of servant quarters |
| `store_rooms` | Number of store rooms |
| `kitchens` | Number of kitchens |

**Total Records:** 300 verified listings
**City:** Islamabad, Pakistan
**Source:** [Zameen.com](https://www.zameen.com)

---

## Data Preprocessing

Raw listings were cleaned through the following steps:

- Columns with more than 50% missing values were dropped
- Numerical columns were filled with the column median; categorical columns with the column mode
- Duplicate rows were removed to prevent training bias
- `price_text` and `size_text` string columns were dropped as their numeric equivalents already exist
- Extreme values at the 99th percentile for price and size were capped to reduce noise
- `location` and `property_type` were encoded numerically using Label Encoding

---

## Exploratory Data Analysis

### Price and Size Distributions

The histograms below show the spread of property prices (in PKR millions) and property sizes (in square feet) after outlier capping.

<img width="1389" height="390" alt="distributions" src="https://github.com/user-attachments/assets/abaf955b-a73b-4dd8-8db0-6b1faa2de06d" />

### Feature Correlation Matrix

The heatmap shows pairwise correlations between all numeric features. `size_sqft` has the strongest correlation with `price_pkr`, followed by `bathrooms` and `bedrooms`.

<img width="663" height="590" alt="correlation" src="https://github.com/user-attachments/assets/a4d533ac-6770-4b70-9c8a-18d00ee7ea98" />

---

## Machine Learning Models

All six models are trained on the same 80/20 train-test split and evaluated using consistent metrics.

| Algorithm | R² Score | RMSE |
|-----------|----------|------|
| CatBoost | 0.895 | PKR 1.86 Crore |
| XGBoost | 0.896 | PKR 2.28 Crore |
| Random Forest | 0.852 | PKR 2.97 Crore |
| Gradient Boosting | 0.802 | PKR 3.18 Crore |
| Decision Tree | 0.781 | PKR 3.96 Crore |
| Linear Regression | 0.724 | PKR 3.98 Crore |

**Winner: CatBoost Regressor** — Best overall balance of R² score (0.895) and lowest error rate (PKR 1.86 Crore RMSE) on real estate pricing data.

### R² Score Comparison

<img width="989" height="490" alt="r2_comparison" src="https://github.com/user-attachments/assets/9091958b-5d63-4e32-a03c-8243a1608e19" />

### Feature Importance (Random Forest)

`size_sqft` is by far the most predictive feature, followed by `location` and `bathrooms`.

<img width="690" height="390" alt="feature_importance" src="https://github.com/user-attachments/assets/85291b25-f51d-4c6f-9361-850d437b3dfb" />

### Actual vs Predicted (Random Forest)

Points cluster tightly along the perfect-prediction diagonal, demonstrating strong model fit across the price range.

<img width="690" height="690" alt="actual_vs_predicted" src="https://github.com/user-attachments/assets/b020ffdc-2e59-4be7-8402-e154bbb68081" />

---

## Model Evaluation

### All Metrics — MAE, MSE, RMSE, R²

The panel below compares all six models across all four evaluation metrics simultaneously.

<img width="1385" height="1014" alt="model_evaluation" src="https://github.com/user-attachments/assets/8868d49a-287b-4f09-9a2a-ee05cd91cd70" />

### Residual Plot

Residuals are evenly scattered around zero with no systematic bias, confirming the model generalises well and does not overfit.

<img width="790" height="490" alt="residuals" src="https://github.com/user-attachments/assets/67f0cd7f-8fa6-4cec-b4bd-c99cc7e0b33e" />

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Language | Python 3.10+ |
| Web Framework | Flask 3.1 |
| ML Libraries | Scikit-learn, XGBoost, CatBoost |
| Data Processing | Pandas, NumPy |
| Frontend | HTML5, Vanilla CSS, Vanilla JavaScript |
| Charts | Chart.js |
| Scraper | Selenium, Requests, BeautifulSoup |

---

## Project Structure

```
PropPredict/
│
├── app.py                          # Flask server — ML pipeline and REST APIs
├── zameen_data.csv                 # Scraped dataset (300 listings)
├── zameen_scraper_v2.ipynb         # CLO-1: Web Scraping Notebook
├── zameen_ml_pipeline.ipynb        # CLO 2-5: Full ML Pipeline Notebook
│
├── templates/
│   └── index.html                  # Single-page dashboard frontend
│
├── static/
│   ├── css/
│   │   └── style.css               # Responsive design system
│   ├── js/
│   │   └── main.js                 # Tab routing, Chart.js, API logic
│   └── images/
│       ├── workflow_poster.png
│       ├── distributions.png
│       ├── correlation.png
│       ├── r2_comparison.png
│       ├── feature_importance.png
│       ├── actual_vs_predicted.png
│       ├── model_evaluation.png
│       └── residuals.png
│
└── README.md
```

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/PropPredict.git
cd PropPredict
```

### 2. Install Dependencies

```bash
pip install flask pandas numpy scikit-learn xgboost catboost
```

### 3. Run the Flask Server

```bash
python app.py
```

### 4. Open in Browser

```
http://127.0.0.1:5000
```

The server will automatically load `zameen_data.csv`, preprocess the dataset, and train all six ML models on startup. This takes approximately 5–10 seconds.

---

## API Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| `GET` | `/` | Serves the dashboard |
| `GET` | `/api/analytics` | Returns market analytics and hotspot data |
| `POST` | `/api/predict` | Predicts house price using the CatBoost model |
| `GET` | `/api/models` | Returns R² and RMSE scores for all six models |
| `GET` | `/api/explorer` | Returns filtered property listings |
| `POST` | `/api/retrain` | Triggers live model retraining |

### Example Prediction Request

```json
POST /api/predict
{
  "area_sqft": 4500,
  "location": "DHA Defence Phase 2, DHA Defence",
  "bedrooms": 5,
  "bathrooms": 6,
  "property_type": "House"
}
```

### Example Response

```json
{
  "estimated_price": "PKR 13.42 Crore",
  "low_bound": "PKR 11.41 Crore",
  "high_bound": "PKR 15.43 Crore",
  "model_version": "CatBoost ML Model v2.4",
  "r2_score": 0.895
}
```

---

## Contributors

Name : **Menahil Suleman**

