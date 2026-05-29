![Stock Market Prediction Banner](header.png)

📈 Stock Market Forecasting Dashboard
### ARIMAX, Naive & XGBoost — Live Predictions for Any Stock

![R Shiny](https://img.shields.io/badge/R-Shiny-276DC3?logo=r)
![Docker](https://img.shields.io/badge/Docker-Deployed-2496ED?logo=docker)
![Live](https://img.shields.io/badge/App-Live-brightgreen)
![quantmod](https://img.shields.io/badge/Data-quantmod%20%2F%20Yahoo%20Finance-blue)

**🔗 Live App:**
- Primary: [stockmarketprediction-uqi4.onrender.com](https://stockmarketprediction-uqi4.onrender.com/)
- Backup: [asmita-desai.shinyapps.io/stockmarketprediction](https://asmita-desai.shinyapps.io/stockmarketprediction/)

📌 What This Does

Enter any stock ticker, pick a date range and forecast horizon, and this dashboard
will pull live price data and run three forecasting models side by side — letting you
compare their predictions, confidence levels, and behavior in a single view.

It's not just a prediction tool. It's a model comparison platform that helps you
understand *how* different approaches handle stock trends, seasonality, and volatility.

Models

### ARIMAX (Time-Series + Exogenous Variable)
- Uses `auto.arima()` with **trading volume as the exogenous regressor**
- Captures trend, seasonality, and volume-driven price signals
- Outputs AIC and (p,d,q) order in the Model Summary sidebar

### Naive (Baseline)
- Assumes the next price = last observed price (random walk)
- Useful as a sanity check — a good model should consistently beat this

### XGBoost (Machine Learning)
- Features: `lag1`, `lag2` (prior day prices), and `volume`
- Trained on 80% of historical data, tested on the remaining 20%
- 50 boosting rounds, adapts dynamically to recent market behavior

📊 Dashboard Features

- **KPI Cards** — Latest price, 30-day average, std dev, max, min, price range
- **Live Forecast KPIs** — Next-day predictions from all three models at a glance
- **Stock Price Chart** — Historical adjusted closing prices for selected ticker
- **Forecast Plot** — All three model forecasts overlaid (ARIMAX blue, Naive green, XGBoost red)
- **Model Forecast Breakdown** — Individual panel per model for detailed view
- **Prediction Focus Donut Chart** — Relative weight/focus allocation across models
- **Model Confidence Spider Chart** — Multi-axis comparison of model reliability
- **Model Summary Sidebar** — AIC, ARIMA order, RMSE per model, interpretive notes

Tech Stack

- **R + Shiny** — app framework and UI
- **quantmod** — live stock data via Yahoo Finance
- **forecast** — ARIMAX via `auto.arima()`, Naive model
- **xgboost** — gradient boosting on lag + volume features
- **ggplot2** — all visualizations
- **fmsb** — spider/radar chart for model confidence
- **Docker** — containerized deployment via Render
- **ShinyApps.io** — backup cloud deployment

Run Locally

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/stock-market-prediction-dashboard.git
cd stock-market-prediction-dashboard

# Install R packages (run once)
Rscript install.R

# Launch the app
Rscript run.R
# or in RStudio: shiny::runApp()
```

Access at `http://127.0.0.1:xxxx` in your browser.

Run with Docker

```bash
docker build -t stock-dashboard .
docker run -p 3838:3838 stock-dashboard
# Access at http://localhost:3838
```

Future Work

- Extend to multi-ticker comparison in a single view
- Add LSTM / Prophet as additional forecasting models
- Include technical indicators (RSI, MACD, Bollinger Bands) as XGBoost features
- Add portfolio-level forecasting across multiple holdings
- Enable downloadable forecast reports (PDF/CSV)

👥 Team

Samir Abdaljalil · Asmita Desai · *(add remaining team members)*

*Texas A&M University — Course Project*

Data Source

Live stock data pulled via [`quantmod`](https://www.quantmod.com/) from Yahoo Finance.
No static datasets — all prices are fetched in real time at app load.
