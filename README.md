<div align="center">

<img src="static/images/workflow_poster.png" alt="PropPredict Workflow" width="100%"/>

<h1>🏠 PropPredict — Islamabad House Price Prediction System</h1>

<p><strong>End-to-end Machine Learning system that scrapes Zameen.com, trains 6 regression models, and predicts house prices in Islamabad through a live interactive web dashboard.</strong></p>

<p>
  <img width="690" height="390" alt="image" src="https://github.com/user-attachments/assets/225f779f-ab56-48a2-94b1-7e2f9a95a0c7" />
  <img src="https://img.shields.io/badge/Flask-3.1-lightgrey?style=flat-square&logo=flask" />
  <img src="https://img.shields.io/badge/CatBoost-R²%200.895-success?style=flat-square" />
  <img src="https://img.shields.io/badge/Dataset-300%20Listings-blue?style=flat-square" />
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=flat-square" />
</p>

</div>

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Workflow](#-workflow)
- [Dashboard Preview](#-dashboard-preview)
- [Dataset](#-dataset)
- [Machine Learning Models](#-machine-learning-models)
- [Model Comparison](#-model-comparison)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [API Endpoints](#-api-endpoints)
- [Contributors](#-contributors)

---

## 🧠 Project Overview

**PropPredict** is a complete house price prediction system built for **Islamabad, Pakistan**, developed as part of a Machine Learning course final project.

The system covers the full data science pipeline:

| Step | Description |
|------|-------------|
| 🕷️ **Data Scraping** | 300+ property listings scraped from Zameen.com |
| 🧹 **Preprocessing** | Missing value handling, outlier capping, label encoding |
| 🤖 **Model Training** | 6 regression algorithms trained and evaluated |
| 📊 **Evaluation** | MAE, MSE, RMSE, and R² scores computed for all models |
| 🌐 **Web Dashboard** | Flask-powered interactive prediction system |

---

## 🔄 Workflow

<div align="center">
<img src="static/images/workflow_poster.png" alt="ML Pipeline Workflow" width="90%"/>
</div>

The pipeline flows from **Zameen.com scraping → CSV storage → data cleaning → model training → live web prediction dashboard**.

---

## 🖥️ Dashboard Preview

The PropPredict dashboard features 4 interactive tabs:

### 📈 Analytics Tab — Islamabad Market Overview
<div align="center">
<img src="static/images/islamabad_map.png" alt="Islamabad Market Overview" width="80%"/>
</div>

> Visualizes property price trends, bedroom distribution, and regional sector hotspots across Islamabad.

---

### 🏠 Property Explorer
<div align="center">
<img src="static/images/dha_house.png" alt="DHA Property Listing" width="45%"/> &nbsp;
<img src="static/images/e11_villa.png" alt="E-11 Villa Listing" width="45%"/>
</div>

> Browse available listings, filter by sector or property type (House, Flat, Farm House), and view premium property cards with real pricing data.

---

### 🏢 Luxury Flat Listings
<div align="center">
<img src="static/images/centaurus_flat.png" alt="Centaurus Apartment" width="80%"/>
</div>

---

### 🤖 Model Performance Matrix
<div align="center">
<img src="static/images/model_comparison_chart.png" alt="Model Comparison Chart" width="80%"/>
</div>

> Live comparison of all 6 ML models with R² and RMSE metrics. Includes an on-demand **Retrain** button to run fresh model training splits.

---

## 📦 Dataset

Property listings scraped from **Zameen.com** for Islamabad (2024).

| Feature | Description |
|---------|-------------|
| `price_pkr` | Property price in Pakistani Rupees (target variable) |
| `location` | Sector/area in Islamabad (e.g., DHA, E-11, F-7) |
| `bedrooms` | Number of bedrooms |
| `bathrooms` | Number of bathrooms |
| `size_sqft` | Total area in square feet |
| `property_type` | House / Flat / Farm House |
| `built_year` | Year of construction |
| `parking_spaces` | Number of parking spaces |
| `servant_quarters` | Number of servant quarters |
| `store_rooms` | Number of store rooms |
| `kitchens` | Number of kitchens |

**Total Records:** 300 verified listings  
**City:** Islamabad, Pakistan  
**Source:** [Zameen.com](https://www.zameen.com)

---

## 🤖 Machine Learning Models

All 6 models are trained on an 80/20 train-test split with the same features and evaluated using consistent metrics.

| Algorithm | R² Score | RMSE |
|-----------|----------|------|
| **CatBoost** ⭐ | **0.895** | PKR 1.86 Crore |
| XGBoost | 0.896 | PKR 2.28 Crore |
| Random Forest | 0.852 | PKR 2.97 Crore |
| Gradient Boosting | 0.802 | PKR 3.18 Crore |
| Linear Regression | 0.724 | PKR 3.98 Crore |
| Decision Tree | 0.781 | PKR 3.96 Crore |

> **Winner: CatBoost Regressor** — Best overall performance with an R² of 0.895 and the lowest error rate on real estate pricing data.

---

## 📊 Model Comparison

<div align="center">
<img src="static/images/model_comparison_chart.png" alt="R² Score Comparison" width="85%"/>
</div>

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| **Language** | Python 3.10+ |
| **Web Framework** | Flask 3.1 |
| **ML Libraries** | Scikit-learn, XGBoost, CatBoost |
| **Data Processing** | Pandas, NumPy |
| **Frontend** | HTML5, Vanilla CSS, Vanilla JavaScript |
| **Charts** | Chart.js |
| **Fonts** | Google Fonts (Outfit, Inter) |
| **Icons** | FontAwesome 6 |
| **Scraper** | Selenium / Requests + BeautifulSoup |

---

## 📁 Project Structure

```
PropPredict/
│
├── app.py                          # Flask server — ML pipeline + REST APIs
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
│       ├── workflow_poster.png     # ML pipeline workflow diagram
│       ├── model_comparison_chart.png  # Model evaluation chart
│       ├── islamabad_map.png       # Regional density map
│       ├── dha_house.png           # DHA property image
│       ├── e11_villa.png           # E-11 villa image
│       └── centaurus_flat.png      # Centaurus flat image
│
└── README.md
```

---

## 🚀 Getting Started

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

> The server will automatically load `zameen_data.csv`, preprocess the dataset, and train all 6 ML models on startup (takes approximately 5–10 seconds).

---

## 🔌 API Endpoints

| Method | Route | Description |
|--------|-------|-------------|
| `GET` | `/` | Serves the dashboard SPA |
| `GET` | `/api/analytics` | Returns market analytics and hotspot data |
| `POST` | `/api/predict` | Predicts house price using CatBoost model |
| `GET` | `/api/models` | Returns R² and RMSE scores for all 6 models |
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

## 👩‍💻 Contributors

| Name | Registration No | University |
|------|-----------------|------------|
| **Menahil Suleman** | FA24-BDS-029 | COMSATS University Islamabad, Virtual Campus |

**Program:** Bachelor of Data Science  
**Course:** Machine Learning Final Project  
**Supervisor:** COMSATS CUI Virtual Campus

---

<div align="center">

Made with 💚 in Islamabad, Pakistan

</div>
