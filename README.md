# Python + Tableau Near Real-Time Crypto Dashboard

## 📊 Project Overview

This project is a near real-time cryptocurrency analytics pipeline built with Python and Tableau.
It continuously fetches cryptocurrency prices from the CoinGecko API every minute, enhances the raw data with rolling averages, volatility, and percent change, and stores the results in a CSV file that powers an interactive Tableau dashboard.

While not a full streaming pipeline (e.g., Kafka/Spark), this project simulates real-time analytics by automating continuous data ingestion and providing dashboards that refresh dynamically.

  * Data Source: CoinGecko API (cryptocurrency prices, 24h % change, trading volume)
  * Data Streaming: Fetches minute-level data to mimic real-time streaming
  * Libraries Used: Requests, Pandas, Datetime, Time, OS.
  * Functionality: Fetches live price data for multiple cryptocurrencies data with rolling averages and volatility measures.
  * Goal: Near-real data feed for real-time analytics for live dashboards.
  * Write-up: The complete walkthrough and code are published here.

<!-- 📂 Data Source

CoinGecko API (cryptocurrency prices, 24h % change, trading volume)

Fetches minute-level data to mimic real-time streaming

🛠️ Tech Stack

Python (Requests, Pandas, Datetime, Time, OS)

Tableau Public (interactive dashboards)

CSV files (staging layer for Tableau connection)

⚙️ Functionality

✔️ Fetches live price data for multiple cryptocurrencies every minute
✔️ Enhances raw API data with:

Rolling averages (5-min, 15-min)

Volatility measures

% change vs. previous record
✔️ Saves updated records into a CSV file (simulating a real-time feed)
✔️ Tableau connects to the CSV and refreshes automatically for live dashboards -->!

🚀 Results

The final Tableau dashboard provides:

Live Line Chart – Real-time prices over time for selected coins

24h % Change Heatmap – Compare relative performance across coins

Volatility Trend Chart – Identify the most stable vs. most volatile assets

KPI Cards – Current price, 24h change, and trading volume

Dashboard Layout (conceptual):

 --------------------------------------------------------
|   ⚡ Crypto Dashboard – Near Real-Time Monitoring      |
|--------------------------------------------------------|
|  KPIs:  Bitcoin $XX,XXX (+2.3%) | Ethereum $X,XXX ... |
|--------------------------------------------------------|
|  Line Chart: Prices over Time (per coin)               |
|--------------------------------------------------------|
|  Heatmap: 24h % Change by Coin                         |
|--------------------------------------------------------|
|  Volatility & Rolling Avg Comparison                   |
 --------------------------------------------------------

🔍 Key Highlights

📡 API Integration – Pulls live market data directly from CoinGecko

⏱ Near Real-Time Updates – Fetches new records every minute

📊 Advanced Metrics – Rolling averages, volatility, and % changes

🎨 Interactive Dashboards – Built with Tableau Public

🧩 ETL Workflow – Extract → Transform → Load into Tableau

📜 Example Code Snippet
def fetch_data():
    url = "https://api.coingecko.com/api/v3/simple/price"
    params = {
        "ids": ",".join(coins),
        "vs_currencies": "usd",
        "include_24hr_change": "true",
        "include_24hr_vol": "true"
    }
    response = requests.get(url, params=params)
    data = response.json()
    
    rows = []
    for coin in coins:
        rows.append({
            "timestamp": datetime.utcnow().strftime("%Y-%m-%d %H:%M:%S"),
            "coin": coin,
            "price_usd": data[coin]["usd"],
            "pct_change_24h": data[coin].get("usd_24h_change", 0),
            "volume_24h": data[coin].get("usd_24h_vol", 0)
        })
    
    return pd.DataFrame(rows)

🖼️ Sample Data Output
timestamp	coin	price_usd	pct_change_24h	volume_24h	rolling_avg_5min	volatility_15min
2025-08-16 17:01:00	bitcoin	61234.56	2.34	348923412.0	61012.34	0.015
2025-08-16 17:01:00	ethereum	3421.78	1.12	23123123.0	3410.55	0.022
2025-08-16 17:01:00	dogecoin	0.083	-0.45	9432134.0	0.081	0.034
📈 Tableau Dashboard

Built with Tableau Public

Connects directly to the continuously updated CSV

Provides near real-time, interactive monitoring of multiple cryptocurrencies

✅ This project demonstrates end-to-end analytics skills:

Data Engineering (API, ETL pipeline)

Data Transformation (feature engineering with Pandas)

Data Visualization (dashboards in Tableau)
