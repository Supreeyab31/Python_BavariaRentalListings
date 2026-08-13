# 🏠 Bavaria Rental Listings EDA — German Real Estate Market Insights

An Exploratory Data Analysis of **235,930 rental listings** across Bavaria (2023) collected from major German real estate platforms. Focused on data quality auditing, missingness profiling, outlier trimming, and rental price per $\text{m}^2$ scaling dynamics. Built as a 3-person team project (**Timon Fetting**, **Supreeya Boriphonmongkol**, **Mahshad Gomar**) for the Python Programming course at KU Eichstätt-Ingolstadt.

## 📦 Technologies

- `Python 3.11`
- `Pandas`
- `NumPy`
- `Matplotlib`
- `Seaborn`
- `ast` / `functools.lru_cache`
- `Jupyter Notebook`

## 🦄 Features

Here is what was accomplished in this project:

- **Data Quality Audit**: Re-calculated listing duration directly from raw timestamp deltas (`lastSeen` − `firstSeen`), fixing calculation errors found in raw crawl metadata (`daysActive_clean`).
- **High-Performance Parsing**: Implemented `lru_cache` + `ast.literal_eval` to parse stringified JSON/dict fields across 235k+ rows with ~10x speedup.
- **NMAR Missingness Profiling**: Demonstrated platform-dependent missingness (Not Missing At Random), avoiding flawed zero/median imputations.
- **Near-Duplicate Detection**: Identified syndicated cross-platform listings via composite hash keys (`title` + `zip` + `price` + `area`).
- **Quantile Outlier Trimming**: Applied 1st–99th percentile trimming on `price` and `area` to remove crawl artifacts while preserving valid market distributions.
- **Regional & Amenity Scaling**: Analyzed price per $\text{m}^2$ scaling non-linearities, city rent rankings (Munich, Nuremberg, Augsburg), and amenity premiums (balcony, lift, furnished status).

## 👨‍🍳 The Process

- **Ingestion & Deserialization**: Efficiently parsed stringified Python objects (`platforms`, `location`, `offerer`) for 235k+ rows using LRU caching.
- **Metric Verification**: Audited `daysActive` against timestamp deltas; derived clean, auditable duration metrics (`daysActive_clean`).
- **Missingness Audit**: Proved missingness is platform-schema dependent (NMAR); applied pairwise deletion and focused on cold rent (`price`).
- **Outlier Strategy**: Evaluated log distributions and 1st–99th quantile trimming vs winsorization to protect correlation validity.
- **Hypothesis Testing**: Answered 5 core market questions covering platform pricing, duration vs price quartiles, area scaling, amenity premiums, and offerer types.

## 📚 What We Learned

During this project, our team acquired vital technical skills and deep statistical domain knowledge:

### 🧠 Data Auditing & Cleaning:
- **Data Skepticism**: Taught us never to trust pre-calculated crawl fields; verify against raw primary timestamps.
- **Missingness Strategy**: Missing attributes reflect scraper schemas (NMAR), making zero/mean imputation invalid.

### 📐 Statistical Methods:
- **Robust Correlation**: Used Spearman rank correlation alongside Pearson to handle heavily right-skewed real estate metrics.
- **Non-Linear Scaling**: Discovered micro-apartments ($\le 30\text{ m}^2$) command significantly higher rent per $\text{m}^2$ than large flats.

### ⚡ Code Optimization:
- **Caching Efficiency**: Leveraged `functools.lru_cache` to eliminate CPU bottlenecks when parsing stringified dicts/lists.

### 🏙️ Real Estate Domain Insights:
- **Urban Premiums**: Quantified major furnished & location premiums in Munich vs mid-sized Bavarian cities.

## 📈 Overall Growth

Working as a 3-person team allowed us to cross-validate data transformation decisions, challenge missingness assumptions, and turn 235k+ uncleaned web-scraped listings into clean, defensible market intelligence.

## 💭 How can it be improved?

- **Geospatial Heatmaps**: Add interactive `GeoPandas` / `Folium` price-per-$\text{m}^2$ maps by postal code (`PLZ`).
- **Predictive ML Model**: Train a LightGBM / XGBoost regression pipeline for rental price estimation.
- **NLP Text Mining**: Extract hidden property amenities from listing titles and description texts.
- **Interactive Dashboard**: Build a `Streamlit` web app for real-time market filtering and cost estimation.

## 🚦 Running the Project

To run the project in your local environment, follow these steps:

1. **Clone the repository**

2. **Install dependencies**:
   ```bash
   pip install pandas numpy matplotlib seaborn jupyter
   ```
3. **Launch the Jupyter Notebook**:
   ```bash
   jupyter notebook Bavaria_Rental_Listings_EDA_TimonChingMahshad.ipynb
   ```

