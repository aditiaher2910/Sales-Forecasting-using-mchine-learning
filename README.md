# 📈 Sales Forecasting with Machine Learning

A time series sales forecasting project that predicts future monthly sales using a **Linear Regression** model built on supervised learning techniques. The project includes data preprocessing, feature engineering, model training, evaluation, and a **Power BI dashboard** for visualization.

---

## 🗂️ Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Project Workflow](#project-workflow)
- [Models Used](#models-used)
- [Results](#results)
- [Power BI Dashboard](#power-bi-dashboard)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Technologies Used](#technologies-used)
- [Future Improvements](#future-improvements)

---

## 📌 Overview

This project tackles the problem of retail sales forecasting by transforming raw transactional data into a supervised learning problem. Daily sales data is aggregated to monthly level, differenced to make it stationary, and then converted into lag features for model training. The trained model predicts the next 12 months of sales, which are then compared against actual values and visualized in Power BI.

---

## 📦 Dataset

- **Source:** Kaggle — Store Item Demand Forecasting Challenge (`train.csv`)
- **Original columns:** `date`, `store`, `item`, `sales`
- **After preprocessing:** `date`, `sales` (aggregated monthly)
- **Date range:** 2013 – 2017 (monthly aggregated)
- **Target variable:** `sales` (total monthly units sold)

---

## 🔄 Project Workflow

```
Raw Data (train.csv)
        │
        ▼
  Data Cleaning
  (drop store & item columns, parse dates)
        │
        ▼
  Monthly Aggregation
  (group by month, sum sales)
        │
        ▼
  Stationarity Transform
  (sales_diff = sales.diff())
        │
        ▼
  Supervised Data Preparation
  (12 lag features: month_1 to month_12)
        │
        ▼
  Train / Test Split
  (last 12 months = test set)
        │
        ▼
  MinMax Scaling
  (feature_range = -1 to 1)
        │
        ▼
  Model Training → Linear Regression
        │
        ▼
  Inverse Transform & Reconstruct Sales
        │
        ▼
  Evaluation (RMSE, MAE, R²)
        │
        ▼
  Export CSVs → Power BI Dashboard
```

---

## 🤖 Models Used

| Model | Library | Status |
|---|---|---|
| Linear Regression | scikit-learn | ✅ Implemented |
| Random Forest Regressor | scikit-learn | 🔧 Imported, ready to extend |
| XGBoost RF Regressor | xgboost | 🔧 Imported, ready to extend |
| LSTM Neural Network | TensorFlow / Keras | 🔧 Imported, ready to extend |

> The current implementation uses **Linear Regression** as the primary model. The other models are imported and can be plugged into the same pipeline.

---

## 📊 Results

Model evaluated on the last **12 months** of data:

| Metric | Description |
|---|---|
| **RMSE** | Root Mean Squared Error — average prediction error in sales units |
| **MAE** | Mean Absolute Error — average absolute deviation from actual sales |
| **R²** | Coefficient of determination — how well the model explains variance |

Predictions are reconstructed from the differenced series back to original sales scale using cumulative addition from the last known actual value.

---

## 📊 Power BI Dashboard

The project exports three CSV files that feed a Power BI dashboard:

| File | Contents |
|---|---|
| `monthly_sales.csv` | Historical monthly actual sales |
| `forecast_vs_actual.csv` | Last 12 months — actual vs predicted sales |
| `model_metrics.csv` | RMSE, MAE, R² score |

**Dashboard visuals include:**
- 📈 Line chart — Actual vs Predicted sales over time
- 📊 Clustered bar chart — Monthly sales comparison by year
- 🎯 KPI cards — RMSE, MAE, R² score
- 📉 Area chart — Sales difference (stationarity check) over time
- 🎛️ Slicers — Year filter and date range picker

---

## 📁 Project Structure

```
sales-forecasting/
│
├── Sales_forecasting.ipynb      # Main Jupyter notebook
├── monthly_sales.csv            # Exported: historical monthly sales
├── forecast_vs_actual.csv       # Exported: forecast comparison
├── model_metrics.csv            # Exported: model evaluation metrics
└── README.md                    # Project documentation
```

---

## ⚙️ Installation

1. **Clone the repository**
```bash
git clone https://github.com/your-username/sales-forecasting.git
cd sales-forecasting
```

2. **Install required libraries**
```bash
pip install pandas numpy matplotlib scikit-learn xgboost tensorflow
```

3. **Or install from requirements (if provided)**
```bash
pip install -r requirements.txt
```

4. **Open the notebook**
```bash
jupyter notebook Sales_forecasting.ipynb
```

> If using **Google Colab**, upload the notebook and the dataset (`train.csv`) to `/content/sample_data/` before running.

---

## 🚀 Usage

1. Place `train.csv` in the correct path (`/content/sample_data/train.csv` for Colab)
2. Run all cells in `Sales_forecasting.ipynb` top to bottom
3. The final cells export three CSV files — `monthly_sales.csv`, `forecast_vs_actual.csv`, `model_metrics.csv`
4. Import those CSVs into Power BI Desktop to build the dashboard

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python 3 | Core programming language |
| Pandas | Data manipulation and aggregation |
| NumPy | Numerical operations and array handling |
| Matplotlib | Data visualization in notebook |
| Scikit-learn | Linear Regression, Random Forest, scaling, metrics |
| XGBoost | Gradient boosted tree model (ready to extend) |
| TensorFlow / Keras | LSTM model (ready to extend) |
| Power BI Desktop | Interactive dashboard and reporting |
| Google Colab | Cloud notebook environment |

---

## 🔮 Future Improvements

- [ ] Add **Random Forest** and **XGBoost** models and compare all three in the dashboard
- [ ] Implement **LSTM** model for deep learning based forecasting
- [ ] Add **ARIMA / SARIMA** as a statistical baseline model
- [ ] Hyperparameter tuning using **GridSearchCV**
- [ ] Add **confidence intervals** around the forecast line
- [ ] Expand to **store-level and item-level** forecasting
- [ ] Automate CSV export and Power BI refresh using Python scripts

---

## 🙌 Acknowledgements

- Dataset from [Kaggle — Store Item Demand Forecasting Challenge](https://www.kaggle.com/competitions/demand-forecasting-kernels-only)
- Supervised learning approach inspired by time series lag feature engineering techniques

---

> **Note:** This project was built and tested on Google Colab. File paths may need adjustment if running locally.
