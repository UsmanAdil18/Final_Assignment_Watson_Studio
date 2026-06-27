# 📈 Extracting and Visualizing Stock Data — IBM Watson Studio

A data analysis project completed as part of the **IBM Data Analyst Professional Certificate** on Coursera.  
This project extracts real stock market and revenue data for **Tesla (TSLA)** and **GameStop (GME)** using Python, then visualizes the data through interactive dashboards.

---

## 📌 Project Overview

Extracting and displaying essential data from multiple sources is a core skill in data science.  
In this project, stock price data is pulled via the **yfinance API** and quarterly revenue data is scraped from the web using **BeautifulSoup**, then both datasets are plotted together on an interactive dual-axis graph.

---

## 📁 Project Structure

```
Final_Assignment_Watson_Studio/
│
├── Final_Assignment.ipynb     # Main Jupyter Notebook with all code and output
└── README.md
```

---

## ❓ Questions Covered

| Question | Task |
|---|---|
| Q1 | Extract Tesla stock data using `yfinance` |
| Q2 | Scrape Tesla quarterly revenue data using `BeautifulSoup` |
| Q3 | Extract GameStop stock data using `yfinance` |
| Q4 | Scrape GameStop quarterly revenue data using `BeautifulSoup` |
| Q5 | Plot Tesla stock price vs revenue graph (up to June 2021) |
| Q6 | Plot GameStop stock price vs revenue graph (up to June 2021) |

---

## 🛠️ Technologies Used

| Tool / Library | Purpose |
|---|---|
| `Python 3` | Core programming language |
| `yfinance` | Fetching live/historical stock data from Yahoo Finance |
| `requests` | Downloading HTML content from web pages |
| `BeautifulSoup (bs4)` | Parsing HTML and extracting revenue tables |
| `pandas` | Data manipulation and cleaning |
| `plotly` | Interactive dual-axis stock + revenue charts |
| `matplotlib` | Alternative graph rendering |
| `Jupyter Notebook` | Development and presentation environment |

---

## ⚙️ How It Works

### Step 1 — Extract Stock Data (yfinance)

```python
import yfinance as yf

# Tesla
tesla = yf.Ticker("TSLA")
tesla_data = tesla.history(period="max")
tesla_data.reset_index(inplace=True)

# GameStop
gme = yf.Ticker("GME")
gme_data = gme.history(period="max")
gme_data.reset_index(inplace=True)
```

### Step 2 — Scrape Revenue Data (BeautifulSoup)

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

url = "https://example.com/revenue-page"
response = requests.get(url)
soup = BeautifulSoup(response.text, "html.parser")

tables = soup.find_all("table")
rows = tables[1].find_all("tr")

data = []
for row in rows[1:]:
    cols = row.find_all("td")
    if len(cols) == 2:
        data.append([cols[0].text.strip(), cols[1].text.strip()])

revenue_df = pd.DataFrame(data, columns=["Date", "Revenue"])
revenue_df["Revenue"] = revenue_df["Revenue"].replace({'\$': '', ',': ''}, regex=True)
revenue_df.dropna(subset=["Revenue"], inplace=True)
revenue_df = revenue_df[revenue_df["Revenue"] != ""]
```

### Step 3 — Plot Stock + Revenue Dashboard

```python
make_graph(tesla_data, tesla_revenue, 'Tesla')
make_graph(gme_data, gme_revenue, 'GameStop')
```

Each graph shows:
- **Top panel** — Historical share price over time
- **Bottom panel** — Quarterly revenue in USD millions
- Data filtered up to **June 2021**

---

## 📊 Sample Output

**Tesla Dashboard:**
- Stock price growth from ~$1 (2010) to ~$700 (2021)
- Revenue growth from $98M (2010) to $10.4B (2021 Q1)

**GameStop Dashboard:**
- Stock price spike during the 2021 short squeeze event
- Revenue trend showing retail decline over the years

---

## 🚀 How to Run

### Option 1 — Run in Jupyter Notebook locally

**Install dependencies:**
```bash
pip install yfinance bs4 pandas plotly matplotlib nbformat
```

**Launch the notebook:**
```bash
jupyter notebook Final_Assignment.ipynb
```

### Option 2 — Run in IBM Watson Studio / Google Colab

Upload `Final_Assignment.ipynb` directly and run all cells.  
All required libraries are pre-installed in those environments.

---

## 📚 Course Information

| Field | Detail |
|---|---|
| **Course** | Python Project for Data Science |
| **Certificate** | IBM Data Analyst Professional Certificate |
| **Platform** | Coursera / IBM Skills Network |
| **Instructor** | Joseph Santarcangelo, Azim Hirjani |

---

## 👤 Author

**Muhammad Usman**  
BS Computer Science — University of Karachi  
IBM Data Analyst Certified  
[GitHub](https://github.com/UsmanAdil18) • [LinkedIn](https://www.linkedin.com/in/muhammad-usman-72a03241a/)
