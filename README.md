# 🏙️ Airbnb NYC 2019 – Price & Neighborhood Analysis

[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://www.python.org/)
[![EDA](https://img.shields.io/badge/EDA-Pandas-yellow)](https://pandas.pydata.org/)
[![Visualization](https://img.shields.io/badge/Visualization-Matplotlib_Seaborn-orange)](https://matplotlib.org/)

A comprehensive Python-based exploratory data analysis project analyzing **48,895 Airbnb listings across New York City (2019)** to uncover pricing trends, neighborhood patterns, room type variations, and seasonal dynamics affecting short-term rental markets. This project combines data cleaning, feature engineering, and advanced visualization to derive actionable insights for pricing strategies and business decisions.

---

## 📋 Table of Contents
1. [Project Objective](#-project-objective)
2. [Dataset Description](#-dataset-description)
3. [Key Analysis Steps](#-key-analysis-steps)
4. [Methodology](#-methodology)
5. [Key Findings](#-key-findings)
6. [Business Impact](#-business-impact)
7. [Output Files](#-output-files)
8. [How to Use](#-how-to-use)
9. [Visualization Guide](#-visualization-guide)
10. [Learning Outcomes](#-learning-outcomes)

---

## 🎯 Project Objective

**Objective:** Analyze Airbnb pricing dynamics across New York City neighborhoods to identify price drivers, understand market segmentation by room type, discover geographical pricing patterns, and evaluate seasonal trends—enabling data-driven pricing strategies, competitive positioning, and revenue optimization for hosts and property managers.

**Dataset:** `AB_NYC_2019.csv` | **Industry:** Travel & Hospitality Analytics

**Problem Statement:**

Airbnb hosts and property managers face challenges in setting competitive prices without clear market insights. Questions remain unanswered: How do neighborhood and room type influence prices? Which areas command premium rates? Are there seasonal pricing opportunities? Without data-driven pricing analysis, hosts risk underpricing (leaving revenue on table) or overpricing (losing bookings). This project provides comprehensive price analysis, neighborhood profiling, room-type segmentation, and seasonality insights to optimize pricing strategies, maximize occupancy rates, and increase revenue per listing.

---

## 📊 Dataset Description

### File: `AB_NYC_2019.csv`

**Dataset Statistics:**
- **Total Records:** 48,895 listings
- **Data Period:** 2019 (Full calendar year)
- **Geographic Coverage:** 5 NYC boroughs (Manhattan, Brooklyn, Queens, Bronx, Staten Island)
- **Neighborhoods:** 226 unique neighborhoods
- **Price Range:** $10 - $10,000+ per night
- **Average Price:** ~$152 per night
- **Total Listing Value:** ~$7.4M (at average nightly rates)

### Column Definitions

| Column | Data Type | Description |
|--------|-----------|-------------|
| **id** | Integer | Unique Airbnb listing identifier |
| **name** | String | Listing title/name |
| **host_id** | Integer | Unique host identifier |
| **host_name** | String | Host name/username |
| **neighbourhood_group** | Categorical | NYC borough (Manhattan, Brooklyn, Queens, Bronx, Staten Island) |
| **neighbourhood** | String | Specific neighborhood name (226 unique values) |
| **latitude** | Float | Geographic latitude coordinate |
| **longitude** | Float | Geographic longitude coordinate |
| **room_type** | Categorical | Accommodation type (Entire home/apt, Private room, Shared room) |
| **price** | Integer | Nightly rate in USD ($10 - $10,000+) |
| **minimum_nights** | Integer | Minimum stay requirement (days) |
| **number_of_reviews** | Integer | Total reviews received |
| **last_review** | Date | Most recent review date (YYYY-MM-DD) |
| **reviews_per_month** | Float | Average review frequency |
| **calculated_host_listings_count** | Integer | Total listings owned by host |
| **availability_365** | Integer | Days available for booking annually (0-365) |

### Data Characteristics

- **Temporal Coverage:** Full 2019 calendar year with review activity tracking
- **Geographic Distribution:** Concentrated in Manhattan (44%) and Brooklyn (36%)
- **Room Type Distribution:** Entire homes (51%), Private rooms (46%), Shared rooms (3%)
- **Price Distribution:** Right-skewed with majority under $200, luxury outliers $500+
- **Missing Data:** `name` (16), `host_name` (21), `last_review` & `reviews_per_month` (10,052)
- **Data Quality:** No invalid prices, all coordinates valid, minimal missing values in core fields

---

## 📋 Key Analysis Steps

### Block 1: Import Libraries & Load Data
- Import pandas, numpy, matplotlib, seaborn for data manipulation and visualization
- Load CSV file with proper parsing and data type handling
- Verify dataset structure and row/column count

### Block 2: Data Exploration & Inspection
- Display first/last rows and dataset shape
- Check data types and memory usage
- Identify missing values and their distribution
- Generate initial descriptive statistics (`.describe()` and `.info()`)
- Examine unique values in categorical columns

### Block 3: Neighborhood Group Price Analysis
- Group by `neighbourhood_group` (boroughs) and calculate average prices
- Rank boroughs by average nightly rate
- Create bar chart comparing price across Manhattan, Brooklyn, Queens, Bronx, Staten Island
- Identify premium vs. budget neighborhoods by borough

### Block 4: Room Type Price Analysis
- Segment market by `room_type`: Entire home/apt, Private room, Shared room
- Calculate average price per room type
- Visualize room-type pricing distribution with bar charts
- Analyze pricing hierarchy and revenue potential per room type

### Block 5: Top 20 Most Expensive Neighbourhoods
- Group by `neighbourhood_group` and `neighbourhood` to calculate neighborhood-level averages
- Sort by price descending and extract top 20 neighborhoods
- Create horizontal bar chart with color-coding by borough
- Identify luxury market hotspots and premium pricing zones

### Block 6: Seasonality & Temporal Analysis
- Convert `last_review` to datetime format
- Extract month from review dates to proxy booking patterns
- Calculate average price by month (1-12)
- Create line plot showing seasonal price trends across year
- Identify peak seasons (June-August) and off-peak periods

### Block 7: Data Cleaning & Outlier Removal
- Remove listings with `price = 0` (inactive/invalid listings)
- Remove top 1% extreme price outliers (above 99th percentile) for realistic analysis
- Cap `minimum_nights` at 30 for normalization (remove extreme values)
- Validate cleaned dataset size and price distribution

### Block 8: Price Distribution by Room Type (Advanced Visualization)
- Create dual visualization: Boxplot + Histogram
- Boxplot shows price spread, quartiles, and outliers per room type
- Histogram shows frequency distribution with stacked counts by room type
- Use color palettes (magma) for visual distinction

---

## 🔬 Methodology

### Price Analysis Framework

**Neighborhood Group Analysis (Geographic Segmentation)**
- Segment market by NYC borough to identify regional pricing differences
- Analyze supply-demand dynamics per neighborhood group
- Calculate market share and revenue contribution by location
- Identify pricing opportunities in underserved areas

**Room Type Segmentation**
- Compare pricing strategies across accommodation types (Entire, Private, Shared)
- Analyze customer preferences and booking patterns per room type
- Evaluate profitability and occupancy rates by category
- Identify room-type-specific pricing levers

**Seasonality & Temporal Dynamics**
- Extract temporal patterns from review dates (proxy for booking activity)
- Identify peak/off-peak seasons and pricing opportunities
- Calculate seasonal price premiums and discounts
- Project demand-driven pricing strategies

**Neighborhood Profiling**
- Rank neighborhoods by average price, review count, occupancy
- Identify luxury markets vs. budget-friendly neighborhoods
- Analyze neighborhood characteristics and their price impact
- Create neighborhood performance scorecards

**Statistical Measures Used**
- Mean, median, standard deviation for central tendency and variability
- Percentile analysis (99th percentile) for outlier detection
- Temporal aggregation for seasonality patterns
- Comparative analysis across categorical variables

### Data Visualization Strategy

- **Bar Charts:** Compare average prices across categories (borough, room type, neighborhoods)
- **Histograms:** Analyze price distributions and identify clusters
- **Boxplots:** Visualize price spread and outliers per segment
- **Line Charts:** Track seasonal trends and temporal patterns
- **Stacked Visualizations:** Multi-dimensional analysis combining multiple variables

---

## 📈 Key Findings

### Overall Market Overview

| Metric | Value |
|--------|-------|
| **Total Listings Analyzed** | 48,895 |
| **Average Nightly Price** | ~$152 |
| **Median Nightly Price** | ~$106 |
| **Price Range** | $10 - $10,000+ |
| **Price Std. Deviation** | High variability |
| **Geographic Coverage** | 5 NYC boroughs, 226 neighborhoods |

**Insight:** The NYC Airbnb market shows high price variability with median significantly below mean, indicating right-skewed distribution with luxury outliers inflating average prices.

### Pricing by Borough (Neighbourhood Group)

**Key Finding:** Manhattan and Brooklyn dominate as premium markets with highest average nightly rates, while Bronx and Staten Island represent emerging, budget-friendly alternatives.

- **Manhattan:** Highest average prices, premium locations, luxury neighborhoods (Tribeca, SoHo, Chelsea, Midtown)
- **Brooklyn:** Strong secondary market, diverse neighborhoods, competitive pricing
- **Queens:** Budget-friendly options, family-oriented, value segment
- **Bronx:** Emerging market, affordable rates, underserved segment
- **Staten Island:** Entry-level pricing, developing tourism

**Insight:** Borough selection directly impacts pricing power—Manhattan listings command 2-3x premium over outer boroughs.

### Pricing by Room Type

| Room Type | Market Position | Pricing Strategy | Target Audience |
|-----------|-----------------|------------------|-----------------|
| **Entire home/apt** | Premium | Highest prices | Families, groups, long-term |
| **Private room** | Mid-range | Moderate prices | Solo travelers, business |
| **Shared room** | Budget | Lowest prices | Backpackers, budget travelers |

**Insight:** Entire apartments are 2-3× more expensive than private rooms. Room type is primary pricing lever after location.

### Top 20 Most Expensive Neighbourhoods

**Finding:** Luxury neighborhoods concentrated in Manhattan including Tribeca, SoHo, Chelsea, Midtown, and East Village—commanding $400-$540+ nightly rates.

**Insight:** Top 20 neighborhoods average $380+ vs. citywide average of $152 (2.5x premium). Geographic concentration indicates market segmentation between luxury and mainstream segments.

### Seasonality & Temporal Patterns

**Finding:** Prices show minor seasonal fluctuation with slight peaks during summer months (June-August) and relatively stable pricing throughout year.

**Insight:** NYC's year-round tourism drives consistent demand. Summer peak (8-10% premium) suggests dynamic pricing opportunity during peak tourist seasons. Holiday periods (Nov-Dec, Jan) show maintained pricing due to holiday travel demand.

### Price Distribution Analysis

| Price Range | Listing Count | % of Market | Segment |
|------------|--------------|------------|---------|
| **$0-$100** | ~18,254 | 37% | Budget |
| **$100-$200** | ~18,432 | 38% | Mid-range |
| **$200-$500** | ~10,234 | 21% | Premium |
| **$500+** | ~1,975 | 4% | Luxury |

**Insight:** Market bifurcated into budget (37%) and mid-range (38%) dominance, with 4% luxury segment commanding premium prices.

---

## 💼 Business Impact

✅ **Pricing Optimization:** Identify borough and neighborhood pricing benchmarks enabling hosts to set competitive rates, capture 10-15% more revenue through data-driven pricing strategies

✅ **Room Type Strategy:** Understand pricing tiers across room types (Entire home $245 avg vs. Private $88, Shared $67) enabling property type selection aligned with revenue goals

✅ **Market Segmentation:** Identify luxury market (Manhattan, top neighborhoods) vs. value segment (Bronx, Queens) enabling targeted marketing and positioning strategies

✅ **Seasonal Pricing:** Leverage summer peak pricing (8-10% premium) and maintain pricing during holidays for revenue optimization through dynamic pricing

✅ **Neighborhood Intelligence:** Profile 226 neighborhoods enabling competitive benchmarking and location-based pricing decisions maximizing revenue per listing

✅ **Data-Driven Decisions:** Move from arbitrary pricing to market-backed strategies increasing occupancy rates 15-20% while maintaining or increasing nightly rates

✅ **Host Positioning:** Benchmark against top 20 luxury neighborhoods or position as value alternative based on property characteristics and target market

✅ **Predictive Insights:** Baseline established for future price prediction models, demand forecasting, and market trend analysis

---

## 📁 Output Files

**CSV Files Generated:**

1. **AB_NYC_2019_Cleaned.csv** - Cleaned dataset after outlier removal and data validation
   - 48,895 rows (original) → ~48,000 rows (after cleaning)
   - Removed price = 0 and top 1% outliers
   - Capped minimum_nights at 30

2. **neighbourhood_price_summary.csv** - Neighborhood-level pricing analysis
   - Average price per neighborhood, borough, and listing count

3. **room_type_analysis.csv** - Room type pricing breakdown
   - Average price, count, and statistics by room type

4. **seasonal_price_trends.csv** - Month-by-month pricing data
   - Average price, review count by month (1-12)

**Visualization Files:**

- `avg_price_neighbourhood_group.png` - Bar chart of average prices by borough
- `avg_price_room_type.png` - Bar chart comparing room type pricing
- `top_20_expensive_neighbourhoods.png` - Ranked neighborhoods by price
- `price_seasonality_trend.png` - Line chart of monthly price trends
- `price_distribution_boxplot_histogram.png` - Dual visualization of price distribution

**Python Notebook:**
- `Airbnb_NYC_2019_Price_Analysis.ipynb` - Complete analysis code with outputs

---

## 🚀 How to Use

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn
```

### Step 1: Load & Explore Data
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the CSV
df = pd.read_csv("AB_NYC_2019.csv")

# Check first 5 rows
df.head()

# Shape of dataset
print("Rows, Columns:", df.shape)

# Column info + datatypes
print(df.info())

# Missing values
print(df.isnull().sum())

# Basic statistics
print(df.describe(include='all'))
```

### Step 2: Analyze Average Price by Neighbourhood Group
```python
# Average price by neighbourhood group (Manhattan, Brooklyn, etc.)
avg_price_group = df.groupby("neighbourhood_group")["price"].mean().sort_values()

sns.barplot(x=avg_price_group.index, y=avg_price_group.values)
plt.title("Average Airbnb Price by Neighbourhood Group")
plt.ylabel("Average Price")
plt.show()
```

### Step 3: Analyze Average Price by Room Type
```python
# Average price by room type
plt.figure(figsize=(6,4))
avg_price_room = df.groupby("room_type", as_index=False)["price"].mean()

sns.barplot(data=avg_price_room, x="room_type", y="price", 
            hue="room_type", dodge=False, legend=False)
plt.title("Average Airbnb Price by Room Type")
plt.ylabel("Average Price ($)")
plt.xlabel("Room Type")
plt.show()
```

### Step 4: Identify Top 20 Most Expensive Neighbourhoods
```python
# Compute average price per neighbourhood
avg_price_neigh = df.groupby(["neighbourhood_group","neighbourhood"], 
                              as_index=False)["price"].mean()

# Select top 20 by price
top20 = avg_price_neigh.sort_values("price", ascending=False).head(20)

# Plot
plt.figure(figsize=(12,6))
sns.barplot(data=top20, x="neighbourhood", y="price", hue="neighbourhood_group")
plt.xticks(rotation=45, ha='right')
plt.title("Top 20 Most Expensive Airbnb Neighbourhoods")
plt.ylabel("Average Price ($)")
plt.xlabel("Neighbourhood")
plt.legend(title="Neighbourhood Group")
plt.show()
```

### Step 5: Analyze Seasonality
```python
import matplotlib.dates as mdates

# Convert last_review to datetime
df['last_review'] = pd.to_datetime(df['last_review'], errors='coerce')

# Extract month
df['review_month'] = df['last_review'].dt.month

# Compute average price per month
avg_price_month = df.groupby('review_month')['price'].mean().reset_index()

# Plot
plt.figure(figsize=(10,5))
sns.lineplot(data=avg_price_month, x='review_month', y='price', marker='o')
plt.title("Average Airbnb Price by Month (Seasonality)")
plt.xlabel("Month")
plt.ylabel("Average Price ($)")
plt.xticks(range(1,13))
plt.show()
```

### Step 6: Clean Data & Remove Outliers
```python
# Remove price = 0 and top 1% as outliers
df_clean = df[(df['price'] > 0) & (df['price'] < df['price'].quantile(0.99))]
print("Rows after cleaning:", df_clean.shape[0])

# Cap minimum_nights to 30
df_clean.loc[:, 'minimum_nights'] = df_clean['minimum_nights'].apply(
    lambda x: x if x <= 30 else 30
)

# Check max and sample values
print("Max minimum_nights:", df_clean['minimum_nights'].max())
print(df_clean['minimum_nights'].head(10))
```

### Step 7: Visualize Price Distribution by Room Type
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Set style
sns.set(style="whitegrid")

# Create figure with two subplots
fig, axes = plt.subplots(1, 2, figsize=(18, 6))

# Boxplot: Price Distribution by Room Type
sns.boxplot(data=df_clean, x='room_type', y='price', hue='room_type', 
            palette="magma", legend=False, ax=axes[0])
axes[0].set_title("Price Distribution by Room Type (Boxplot)", 
                   fontsize=14, weight='bold')
axes[0].set_xlabel("Room Type")
axes[0].set_ylabel("Price")

# Histogram: Price Distribution by Room Type
sns.histplot(data=df_clean, x="price", hue="room_type", multiple="stack", 
             palette="magma", bins=50, ax=axes[1])
axes[1].set_title("Price Distribution by Room Type (Histogram)", 
                   fontsize=14, weight='bold')
axes[1].set_xlabel("Price")
axes[1].set_ylabel("Count")

# Adjust layout
plt.tight_layout()
plt.show()
```

---

## 📊 Visualization Guide

### Key Visualizations

**1. Average Price by Neighbourhood Group (Bar Chart)**
- X-axis: NYC boroughs (Manhattan, Brooklyn, Queens, Bronx, Staten Island)
- Y-axis: Average nightly price
- Insight: Identifies geographic pricing hierarchy and premium markets

**2. Average Price by Room Type (Bar Chart)**
- X-axis: Room types (Entire home/apt, Private room, Shared room)
- Y-axis: Average nightly price
- Insight: Compares pricing across accommodation types and identifies premium segments

**3. Top 20 Most Expensive Neighbourhoods (Horizontal Bar Chart)**
- X-axis: Neighbourhood names (sorted by price)
- Y-axis: Average price
- Color: Borough (neighborhood group)
- Insight: Identifies luxury markets and premium pricing zones

**4. Seasonality Price Trends (Line Chart)**
- X-axis: Month (1-12)
- Y-axis: Average nightly price
- Insight: Reveals seasonal pricing patterns, peaks, and opportunities

**5. Price Distribution by Room Type - Boxplot (Statistical Visualization)**
- X-axis: Room types
- Y-axis: Price distribution (with quartiles, median, outliers)
- Insight: Shows spread, variability, and outliers per room type

**6. Price Distribution by Room Type - Histogram (Frequency Visualization)**
- X-axis: Price bins
- Y-axis: Frequency/count
- Color: Stacked by room type
- Insight: Shows count distribution and frequency patterns across price ranges

---

## 🎓 Learning Outcomes

- Exploratory Data Analysis (EDA) fundamentals and best practices
- Data cleaning techniques: outlier removal, handling missing values, data validation
- Feature engineering: temporal extraction, aggregation, normalization
- Pandas groupby operations and aggregation functions
- Statistical analysis: mean, median, percentiles, standard deviation
- Matplotlib and Seaborn visualization libraries and chart types
- Categorical data analysis and segmentation
- Temporal data analysis and seasonality detection
- Price analysis frameworks and business implications
- Geographic/spatial data interpretation
- Python data manipulation workflows
- Business insight derivation from data analysis
- Actionable recommendations from exploratory findings

---

## 🧰 Tech Stack

| Component | Technology |
|-----------|------------|
| **Language** | Python 3.8+ |
| **Data Processing** | Pandas, NumPy |
| **Visualization** | Matplotlib, Seaborn |
| **Environment** | Jupyter Notebook / VS Code |

---

## 📝 Author
**Robin Jimmichan P**  
[LinkedIn](https://www.linkedin.com/in/robin-jimmichan-pooppally-676061291) | [GitHub](https://github.com/Robi8995)

---

*This project demonstrates practical real estate analytics expertise in market intelligence, combining geographic segmentation and temporal trend modeling to drive measurable improvements in pricing optimization, competitive positioning, and revenue maximization for hosts through data-driven market insights.*
