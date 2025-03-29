# Sales Forecasting for Pic'Asso – DataPic

Project conducted as part of the PR (Projet de Recherche) at Université de Technologie de Compiègne (UTC) in 2018-2019.

## Authors

- Alexandre Brasseur  
- Matthieu Glorion  
- Lorys Hamadache

## Objective

Build a time-series-based decision support tool to help forecast sales at Pic'Asso (UTC’s student café), improving supply and reducing waste.

## Dataset

- Source: 5 years of transaction data from PayUTC (via Weezevent)
- Format: Daily sales by product
- Additional features: Manual event calendar (holidays, exams), product info
- Data cleaning:
  - Removed short-lived / duplicate products
  - Merged similar items via Levenshtein distance
  - Filtered down to 376 useful products

## Project Steps

### Data Collection

- Sales: Pulled via PayUTC API using a custom Python client
- Events: Manual CSV calendar + collector
- Products: Retrieved with metadata (price, category, availability)

### Exploratory Analysis

- Patterns found: Weekly & semester-based seasonality, major spikes
- Focus products: Café & Pampryl Apricot (consistent, low variance)

### Tested Models

- **ARIMA**
  - Baseline performance, simple implementation
  - Lacks seasonality handling
- **SARIMA**
  - Captures weekly seasonality
  - Slightly better results than ARIMA
- **SARIMAX**
  - Adds exogenous variables (holidays, exams, cyclic encoding)
  - Improved accuracy and interpretability
- **SARIMAX + Data Transformation**
  - Removed weekends/holidays
  - Best performance overall

### Results Summary

| Model              | AIC     | BIC     | MSE     | Runtime   |
|--------------------|---------|---------|---------|-----------|
| ARIMA              | 14436.3 | 14504.9 | 2401.9  | 8min24s   |
| SARIMA             | 14127.1 | 14164.0 | 2249.3  | 17min13s  |
| SARIMAX            | 14259.8 | 14365.4 | 2015.2  | 46min54s  |
| SARIMAX (cleaned)  | 6508.0  | 6587.2  | 1239.6  | 18min43s  |

### Interface

- Built with **Django** + **Chart.js**
- Features:
  - Product-level forecasts
  - Stock visualization
  - Inventory & order planning (ERP-like logic)
- Modular and ready for future feature additions (e.g. OCR, supplier DB)

## Conclusion

- Clean data + thoughtful modeling improved forecasts significantly
- SARIMAX with transformed series performed best
- A usable tool was built for Pic'Asso to support real-world decisions

## Resources

- 📄 [Full Report (PDF)](./DataPic.pdf)  
- 🧠 [Model Code & Forecast Engine (Private Repo)]  
- 🖥️ [Django Web App (with Charts & ERP tools)]  
