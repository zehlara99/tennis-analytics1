# Tennis Analytics

Statistical analysis of ATP Top 100 players using data scraped from [Tennis Abstract](https://tennisabstract.com).

## What It Does

1. **Scrapes** serve, return, break point, and overall performance stats for ATP Top 50 and Ranks 51–100
2. **Cleans and merges** the data into a single 100-player dataset
3. **Analyzes** the data across 9 areas: distributions, serve, return, break points, correlations, clustering, regression, hypothesis testing, and player spotlights

## Key Findings

- A **1–2% difference in total points won** translates to a 10–15% swing in match win rate (tennis's amplification effect)
- **Dominance Ratio** explains 76% of match win variance in a Random Forest model — it's the single most predictive stat
- The biggest gap between Top 50 and Ranks 51–100 is **break point conversion** (+3.25 pp), not serve power
- K-Means clustering identifies **4 player archetypes**: All-Court Dominators (Alcaraz, Sinner, Djokovic), Big Servers, Counter-Punchers, and Grinders
- Match win rate is **84% predictable** (R²=0.84) from 13 standard stats alone

## Project Structure

```
tennis-analytics/
├── scrape.ipynb          # Scraping + data merging
├── eda.ipynb             # Cleaning + full analysis (9 parts)
├── blog_post.md          # Write-up: "15 Data-Driven Facts About Tennis"
├── data-DD-Mon-YYYY/     # Output folder created per scraping run
│   ├── tennis_leaders_serve.csv          # Top 50 raw serve stats
│   ├── tennis_leaders_51_100_serve.csv   # Ranks 51-100 raw serve stats
│   ├── serve_data.csv                    # Merged (100 players)
│   └── ... (same pattern for return, breaks, more)
└── blog_assets/          # Chart PNGs exported from eda.ipynb
```

## Tech Stack

| Purpose | Libraries |
|---------|-----------|
| Scraping | `selenium`, `beautifulsoup4` |
| Data | `pandas`, `numpy` |
| Visualization | `matplotlib`, `seaborn` |
| Machine Learning | `scikit-learn` (KMeans, PCA, RandomForest, LinearRegression) |
| Statistics | `scipy` (t-test, chi-squared, Pearson r) |

## Setup

```bash
git clone https://github.com/YOUR_USERNAME/tennis-analytics.git
cd tennis-analytics

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

You also need [ChromeDriver](https://chromedriver.chromium.org/) installed and on your PATH (matching your Chrome version).

## How to Run

**Step 1 — Scrape the data**

Open `scrape.ipynb` and run all cells. The notebook will:
- Create a dated folder (`data-DD-Mon-YYYY/`) automatically
- Scrape Top 50 and Ranks 51–100 for each stat category
- Save 8 raw CSVs and 4 merged CSVs (100 rows each)

**Step 2 — Run the analysis**

Open `eda.ipynb` and run all cells. The notebook auto-detects the most recent data folder. It will:
- Clean and validate the data (Part 0)
- Produce all charts and statistical outputs (Parts 1–9)
- Export chart PNGs to `blog_assets/`

## Data Source

All statistics from [Tennis Abstract](https://tennisabstract.com), covering the 2024–2025 ATP season. Data reflects season-to-date stats at the time of scraping.
