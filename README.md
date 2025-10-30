# 🏙️ Airbnb NYC 2019 – Price & Neighborhood Analysis

[![Python](https://img.shields.io/badge/Python-3.8+-blue)](https://www.python.org/)
[![EDA](https://img.shields.io/badge/EDA-Pandas-yellow)](https://pandas.pydata.org/)
[![Visualization](https://img.shields.io/badge/Visualization-Matplotlib_Seaborn-orange)](https://matplotlib.org/)

A comprehensive Python-based exploratory data analysis project analyzing **Airbnb listings in New York City (2019)** to uncover pricing trends, neighborhood patterns, room type variations, and seasonal dynamics. This project combines data cleaning, feature engineering, and visualization to derive actionable insights.

---

## 📋 Table of Contents

- [Project Objective](#project-objective)
- [Dataset Description](#dataset-description)
- [Key Analysis Steps](#key-analysis-steps)
- [Installation & Prerequisites](#installation--prerequisites)
- [How to Use](#how-to-use)
- [Key Findings](#key-findings)
- [Visualization Guide](#visualization-guide)
- [Learning Outcomes](#learning-outcomes)
- [Tech Stack](#tech-stack)

---

## 🎯 Project Objective

Analyze Airbnb pricing across New York City neighborhoods to:

✅ Identify price differences by neighborhood group (borough)  
✅ Analyze pricing variations by room type  
✅ Discover most expensive neighborhoods  
✅ Examine seasonal price patterns  
✅ Provide data-driven pricing insights  

---

## 📊 Dataset Description

### File: `AB_NYC_2019.csv`

**Dataset Statistics:**
- **Total Records:** 48,895 listings
- **After Cleaning:** 48,392 listings
- **Data Period:** 2019
- **Geographic Coverage:** NYC (5 boroughs, 221 neighborhoods)
- **Price Range:** $0 - $10,000 per night
- **Average Price:** $152.72 per night
- **Median Price:** $106 per night

### Column Definitions

| Column | Data Type | Description |
|--------|-----------|-------------|
| id | Integer | Unique listing identifier |
| name | String | Listing title |
| host_id | Integer | Unique host identifier |
| host_name | String | Host name |
| neighbourhood_group | Categorical | NYC borough |
| neighbourhood | String | Specific neighborhood (221 unique) |
| latitude | Float | Geographic latitude |
| longitude | Float | Geographic longitude |
| room_type | Categorical | Entire home/apt, Private room, Shared room |
| price | Integer | Nightly rate in USD |
| minimum_nights | Integer | Minimum stay requirement (days) |
| number_of_reviews | Integer | Total reviews received |
| last_review | Date | Most recent review date |
| reviews_per_month | Float | Average review frequency |
| calculated_host_listings_count | Integer | Total listings owned by host |
| availability_365 | Integer | Days available annually (0-365) |

### Data Quality

**Missing Values (Before Cleaning):**
- name: 16 missing
- host_name: 21 missing
- last_review: 10,052 missing
- reviews_per_month: 10,052 missing
- All other columns: 0 missing

**Data Types:**
- Integer: 7 columns (id, host_id, price, minimum_nights, number_of_reviews, calculated_host_listings_count, availability_365)
- Float: 3 columns (latitude, longitude, reviews_per_month)
- Object: 6 columns (name, host_name, neighbourhood_group, neighbourhood, room_type, last_review)

---

## 🔬 Key Analysis Steps

### Step 1: Load & Explore Data

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the CSV
df = pd.read_csv("AB_NYC_2019.csv")

# Check first 5 rows
print(df.head())

# Shape of dataset
print("Rows, Columns:", df.shape)

# Column info + datatypes
print(df.info())

# Missing values
print(df.isnull().sum())

# Basic statistics
print(df.describe(include='all'))
```

### Step 2: Average Price by Neighbourhood Group

```python
# Average price by neighbourhood group
avg_price_group = df.groupby("neighbourhood_group")["price"].mean().sort_values()

sns.barplot(x=avg_price_group.index, y=avg_price_group.values)
plt.title("Average Airbnb Price by Neighbourhood Group")
plt.ylabel("Average Price")
plt.show()
```

### Step 3: Average Price by Room Type

```python
# Average price by room type
plt.figure(figsize=(6,4))
avg_price_room = df.groupby("room_type", as_index=False)["price"].mean()

sns.barplot(data=avg_price_room, x="room_type", y="price", hue="room_type", dodge=False, legend=False)
plt.title("Average Airbnb Price by Room Type")
plt.ylabel("Average Price ($)")
plt.xlabel("Room Type")
plt.show()
```

### Step 4: Top 20 Most Expensive Neighbourhoods

```python
# Compute average price per neighbourhood
avg_price_neigh = df.groupby(["neighbourhood_group","neighbourhood"], as_index=False)["price"].mean()

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

### Step 5: Seasonality Analysis

```python
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

### Step 6: Data Cleaning & Outlier Removal

```python
# Remove price = 0 and top 1% as outliers
df_clean = df[(df['price'] > 0) & (df['price'] < df['price'].quantile(0.99))]

print("Rows after cleaning:", df_clean.shape[0])
```

### Step 7: Cap Minimum Nights

```python
# Cap minimum_nights to 30
df_clean.loc[:, 'minimum_nights'] = df_clean['minimum_nights'].apply(lambda x: x if x <= 30 else 30)

# Check max and sample values
print("Max minimum_nights:", df_clean['minimum_nights'].max())
print(df_clean['minimum_nights'].head(10))
```

### Step 8: Price Distribution by Room Type

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Set style
sns.set(style="whitegrid")

# Create figure with two subplots
fig, axes = plt.subplots(1, 2, figsize=(18, 6))

# Boxplot: Price Distribution by Room Type
sns.boxplot(data=df_clean, x='room_type', y='price',
            hue='room_type', palette="magma", legend=False, ax=axes[0])
axes[0].set_title("Price Distribution by Room Type (Boxplot)", fontsize=14, weight='bold')
axes[0].set_xlabel("Room Type")
axes[0].set_ylabel("Price")

# Histogram: Price Distribution by Room Type
sns.histplot(data=df_clean, x="price", hue="room_type",
             multiple="stack", palette="magma", bins=50, ax=axes[1])
axes[1].set_title("Price Distribution by Room Type (Histogram)", fontsize=14, weight='bold')
axes[1].set_xlabel("Price")
axes[1].set_ylabel("Count")

# Adjust layout
plt.tight_layout()
plt.show()
```

---

## ⚙️ Installation & Prerequisites

```bash
pip install pandas numpy matplotlib seaborn
```

**Python Version:** 3.8+

---

## 📈 Key Findings

### Overall Market

**Dataset Summary:**
- Total Listings: 48,895
- After Cleaning: 48,392 (503 records removed)
- Average Nightly Price: $152.72
- Median Nightly Price: $106
- Price Range: $0 - $10,000
- Standard Deviation: $240.15

**Insight:** The NYC Airbnb market shows high price variability with median significantly below mean, indicating a right-skewed distribution with luxury outliers.

### Key Statistics

| Metric | Value |
|--------|-------|
| **Count** | 48,895 listings |
| **Mean Price** | $152.72 |
| **Std Deviation** | $240.15 |
| **Min Price** | $0 |
| **25th Percentile** | $69 |
| **Median (50th)** | $106 |
| **75th Percentile** | $175 |
| **Max Price** | $10,000 |

### Room Types (From Data)

Room type categories present in data:
- Entire home/apt
- Private room
- Shared room

### Neighbourhood Groups

5 NYC boroughs:
- Manhattan
- Brooklyn
- Queens
- Bronx
- Staten Island

### Data After Processing

**Minimum Nights Cap:** 30 days (normalized from extreme values)

**Price Outliers Removed:** Top 1% extreme prices removed for realistic analysis

**Final Clean Dataset:** 48,392 listings ready for analysis

---

## 📊 Visualization Guide

| Visualization | Description |
|---------------|-------------|
| **Price by Neighbourhood Group** | Bar chart showing average nightly price by NYC borough |
| **Price by Room Type** | Bar chart comparing prices across room types |
| **Top 20 Neighbourhoods** | Ranked bar chart of most expensive neighborhoods by borough |
| **Seasonality Trend** | Line chart showing average price by month (1-12) |
| **Price Distribution Boxplot** | Statistical visualization showing price spread and outliers by room type |
| **Price Distribution Histogram** | Frequency distribution stacked by room type |

---

## 🎓 Learning Outcomes

✅ Exploratory Data Analysis (EDA) fundamentals

✅ Data cleaning: outlier removal, handling missing values, normalization

✅ Feature engineering: temporal extraction (month from date)

✅ Pandas groupby operations and aggregation

✅ Statistical analysis: mean, median, percentiles, standard deviation

✅ Matplotlib and Seaborn visualization

✅ Categorical data analysis and segmentation

✅ Temporal data analysis and seasonality detection

✅ Data validation and quality checks

✅ Python data manipulation workflows

---

## 📝 Notes

- Data cleaned from 48,895 to 48,392 records (503 records with price=0 or extreme outliers removed)
- Minimum nights normalized to maximum of 30 days
- Datetime parsing applied to last_review column for temporal analysis
- 10,052 missing values in last_review and reviews_per_month columns
- All coordinates and core listing information complete and valid

---

## 🧰 Tech Stack

| Component | Technology |
|-----------|------------|
| **Language** | Python 3.8+ |
| **Data Processing** | Pandas, NumPy |
| **Visualization** | Matplotlib, Seaborn |
| **Environment** | Jupyter Notebook / VS Code |
| **Dataset Used** | AB_NYC_2019.csv |

---

## 📝 Author
**Robin Jimmichan Pooppally**  
[LinkedIn](https://www.linkedin.com/in/robin-jimmichan-pooppally-676061291) | [GitHub](https://github.com/Robi8995)

---

*This project demonstrates practical real estate analytics expertise in market intelligence, combining geographic segmentation and temporal trend modeling to drive measurable improvements in pricing optimization, competitive positioning, and revenue maximization for hosts through data-driven market insights*
