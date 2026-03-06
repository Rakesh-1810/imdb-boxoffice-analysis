# 🎬 IMDB Box Office Gross Analysis

> End-to-end EDA project — web scraping, data cleaning, and revenue insights across 593 top-grossing films (1939–2025)

---

## 📌 Project Overview

This project analyzes worldwide box office revenue patterns using data scraped directly from **Box Office Mojo (IMDB Pro)**. The goal was to uncover how revenue is distributed across domestic and foreign markets, identify top-grossing films, and discover long-term revenue trends over decades.

---

## 🎯 Objectives

- Scrape real-world box office data using Python & BeautifulSoup
- Clean and transform raw scraped data into analysis-ready format
- Identify top-grossing films and revenue concentration patterns
- Understand domestic vs. foreign market dynamics
- Discover year-over-year revenue trends and the impact of key events (Star Wars, COVID-19)

---

## 📊 Dataset

| Property | Value |
|---|---|
| Source | [Box Office Mojo — Top Lifetime Gross](https://www.boxofficemojo.com/chart/top_lifetime_gross/?area=XWW) |
| Movies | 593 (after deduplication) |
| Year Range | 1939 – 2025 |
| Min Gross | ~$300M |
| Max Gross | $2.92B (Avatar) |
| Features | Rank, Name, Worldwide Gross, Domestic Gross, Foreign Gross, Domestic %, Foreign %, Year |

### Dataset Info

![Dataset Info](visuals/data_info.PNG)

---

## 🛠️ Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3 |
| Scraping | `requests`, `BeautifulSoup4` |
| Data Wrangling | `Pandas`, `NumPy` |
| Visualization | `Matplotlib`, `Seaborn` |
| Environment | Jupyter Notebook / Google Colab |

---

## 🔍 Methodology

### 1. Web Scraping
- Scraped 3 paginated pages (offsets 0, 200, 400) from Box Office Mojo
- Mimicked browser headers (`User-Agent`) to bypass anti-scraping measures
- Used `time.sleep(2)` between requests for responsible rate limiting
- Extracted: Rank, Name, WW/Dom/Foreign Gross, %, Year
- Applied `drop_duplicates(subset=['Name'])` to remove cross-page duplicates → **593 unique records**

### 2. Data Cleaning
- Stripped `$` signs and commas from gross columns using `str.replace()`
- Removed `%` symbols from percentage columns
- Cast all numeric columns from `object` → `int64` / `float64`
- Result: **Zero missing values**, fully typed dataset

### 3. Exploratory Data Analysis (EDA)
- Distribution analysis (box plots, histograms)
- Log transformation to handle extreme right-skew
- Pearson correlation between domestic and foreign markets
- Pareto / cumulative revenue concentration analysis
- Year-over-year revenue trend analysis
- Market category segmentation (International Blockbuster / Balanced / Domestic Specialty)

---

## 📈 Visualizations & Insights

### 1. Worldwide Gross Distribution — Outlier Detection
![Worldwide Gross Box Plot](visuals/World_wide_gross_Outliers.png)
> Strong right-skew with blockbuster outliers like Avatar ($2.92B) and Avengers: Endgame ($2.80B). Log transformation was applied for fair statistical comparisons.

---

### 2. Top 10 Movies by Worldwide Gross
![Top 10 Movies](visuals/Top_10_movies.PNG)
> Avatar leads at $2.92B (2009), followed by Avengers: Endgame and Avatar: The Way of Water. Notably, Ne Zha 2 (2025) enters the top 5 — a sign of China's growing box office dominance.

---

### 3. Pareto Analysis — Revenue Concentration
![Pareto Analysis](visuals/Pareto_Analysis_plot.png)
> Unlike the classic 80/20 rule, revenue is distributed **nearly linearly** across all 593 films — meaning there's no extreme concentration at the top. The box office is more competitive than traditional media markets.

---

### 4. Top 5% vs Remaining 95% Revenue Split
![Top 5 vs Remaining](visuals/Top_5_vs_remaining_5_revenuve_plot.png)
> The top 5% of movies generate only **5.34%** of total revenue, confirming the unusually equal distribution found in the Pareto analysis.

---

### 5. Pearson Correlation — Domestic vs Foreign Gross
![Pearson Regression Plot](visuals/pearson_reg_plot.png)
> **Pearson r = 0.08** — domestic and foreign performance are almost entirely uncorrelated. Studios cannot rely on domestic success to predict foreign performance. Independent marketing strategies are essential.

---

### 6. Revenue Efficiency — Foreign Market Reliance vs Worldwide Gross
![Revenue Efficiency](visuals/Revenuve_efficiency__Foriegn_vs_worldwide_.png)
> A positive trend: films with higher foreign market reliance (70%+) tend to generate higher worldwide gross. Global IP and franchise films clearly benefit from international expansion.

---

### 7. Market Category Analysis
![Market Category](visuals/Market_-_Category.PNG)
> **433 films** fall into the "Balanced" category, while **155** are International Blockbusters (>60% foreign revenue). Only **5 films** are primarily domestic-focused — confirming that global appeal is essential for box office success.

---

### 8. Year-over-Year Revenue Growth
![YoY Growth](visuals/YOY_-_Growth.png)
> Key events visible in the data:
> - **1977**: Star Wars effect — massive YoY spike (~100%)
> - **1984**: Indiana Jones / Ghostbusters boom (~95%)
> - **1999**: Matrix / Star Wars prequel surge (~100%)
> - **2020**: COVID-19 — catastrophic ~80% decline
> - **2021–22**: Post-COVID recovery surge (~140%+)

---

### 9. Mean vs Median Gross by Year
![Mean vs Median](visuals/Mean_vs_Median__year_.png)
> Mean and median track closely, indicating consistent data within each year. A sharp spike around 1982 (E.T., Raiders) and 1999 (Phantom Menace) is driven by megablockbusters. The **modern era (2010+) consistently outperforms** all prior periods.

---

## 💡 Key Findings

| # | Insight |
|---|---|
| 🌍 | **73% of top-grossing films** earn more in foreign markets than domestically |
| 📉 | **Domestic–Foreign correlation is only r = 0.08** — markets are nearly independent |
| 📊 | Revenue follows a **linear distribution** (not the classic 80/20 Pareto rule) |
| 🦠 | **COVID-19 caused ~80% decline** in 2020, followed by 140%+ rebound in 2021–22 |
| 📈 | **Post-2010 era consistently outperforms** all prior decades in mean gross |
| 🥇 | **Avatar ($2.92B)** leads — 73% earned from foreign markets |

---

## 📁 Project Structure
```
imdb-boxoffice-analysis/
│
├── data/
│   └── boxoffice_top593.csv          # Cleaned dataset
│
├── notebooks/
│   └── IMDB_Gross_Analysis.ipynb     # Full analysis notebook
│
├── visuals/
│   ├── World_wide_gross_Outliers.png
│   ├── Top_10_movies.PNG
│   ├── Pareto_Analysis_plot.png
│   ├── Top_5_vs_remaining_5_revenuve_plot.png
│   ├── pearson_reg_plot.png
│   ├── Revenuve_efficiency__Foriegn_vs_worldwide_.png
│   ├── Market_-_Category.PNG
│   ├── YOY_-_Growth.png
│   ├── Mean_vs_Median__year_.png
│   └── data_info.PNG
│
└── README.md
```

---

## 🚀 How to Run
```bash
# 1. Clone the repo
git clone https://github.com/-Rakesh-1810/imdb-boxoffice-analysis.git
cd imdb-boxoffice-analysis

# 2. Install dependencies
pip install requests beautifulsoup4 pandas numpy matplotlib seaborn jupyter

# 3. Launch the notebook
jupyter notebook notebooks/IMDB_Gross_Analysis.ipynb
```

> ⚠️ Re-scraping live data may yield slightly different results as Box Office Mojo updates rankings over time.

---

## 🧗 Challenges Faced

- **Anti-scraping measures** — Resolved by sending browser-like `User-Agent` headers
- **Duplicate records** across paginated pages — Resolved using `drop_duplicates(subset=['Name'])`
- **Messy string dtypes** — Multi-step cleaning with `str.replace()` and type casting
- **Extreme right-skew** — Applied log transformation for meaningful statistical comparisons

---

## 📚 Learnings

- Web scraping with BeautifulSoup & handling pagination
- Real-world data cleaning in Pandas
- Log transformation for skewed distributions
- Pearson correlation and what it means for business strategy
- Pareto analysis and challenging assumptions about market concentration
- Responsible scraping with rate limiting

---

## 👤 Author

**Rakesh**
- 🎓 MTech in Data Science
- 💼 [LinkedIn](https://www.linkedin.com/in/rakesh-r%C3%B6%C3%A7ky-852a4926a)
- 🐙 [GitHub](https://github.com/Rakesh-1810)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
