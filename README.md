# 🏠 Real Estate Data Cleaning Pipeline

## 📊 Project Overview
This project processes a large-scale real estate dataset containing **2.2 million property listings** from Realtor.com. The pipeline handles missing values, removes redundant features, and produces clean, analysis-ready datasets.

## 📁 Dataset Information
- **Original rows**: 2,226,382
- **Final rows**: 2,199,643 (99.62% retained)
- **Features**: 10-11 columns (depending on version)
- **Data source**: Realtor.com property listings

## Data URL
https://www.kaggle.com/datasets/ahmedshahriarsakib/usa-real-estate-dataset

## 🎯 Data Cleaning Steps

### 1. Initial Filtering
- Removed rows missing critical fields: `price`, `city`, `state`, `zip_code`, `brokered_by`
- Retained **99.17%** of original data

### 2. Missing Value Imputation
- **City-specific median imputation** for:
  - Number of bedrooms (`bed`)
  - Number of bathrooms (`bath`)
  - Property size (`house_size`)
  - Lot size (`acre_lot`)
- **Fallback**: Dropped remaining 8,338 rows with persistent missing values

### 3. Feature Removal
- **Removed `street` column**: 2,001,358 unique values (99.9% cardinality)
- **Note**: `prev_sold_date` kept as optional feature

### 4. Data Type Optimization
- Converted `status` to categorical type
- Standardized date formats

## 📦 Dataset Versions

### Version 1: With Previous Sale Date
**File**: `housing_data_with_sold_date.csv`
- **Rows**: 2,199,643
- **Columns**: 11
- **Features**: 
  - `brokered_by` - Broker/agency ID
  - `status` - Listing status (for_sale, etc.)
  - `price` - Current listing price
  - `bed` - Number of bedrooms
  - `bath` - Number of bathrooms
  - `acre_lot` - Lot size in acres
  - `city` - Property city
  - `state` - Property state
  - `zip_code` - Postal code
  - `house_size` - Square footage
  - `prev_sold_date` - Previous sale date (67.3% have data)

### Version 2: Without Previous Sale Date
**File**: `housing_data_without_sold_date.csv`
- **Rows**: 2,199,643
- **Columns**: 10
- Same features as above, excluding `prev_sold_date`

## 📈 Data Quality Metrics

| Metric | Value |
|--------|-------|
| **Data retention rate** | 99.62% |
| **Rows with complete data** | 2,199,643 |
| **Missing values after cleaning** | 0 |
| **Unique cities** | 19,675 |
| **Unique zip codes** | 30,334 |
| **Properties with sale history** | 1,479,940 (67.3%) |

## 🔍 Sample Data Preview

| Price | Bed | Bath | House Size | City | Previous Sale |
|-------|-----|------|------------|------|---------------|
| $105,000 | 3 | 2 | 920 sq ft | Adjuntas | Not Previously Sold |
| $80,000 | 4 | 2 | 1,527 sq ft | Adjuntas | Not Previously Sold |
| $145,000 | 4 | 2 | 1,800 sq ft | Ponce | Not Previously Sold |
| $300,000 | 5 | 3 | 5,403 sq ft | Las Marias | Not Previously Sold |

## 🛠️ Technologies Used

- **Python 3.13**
- **Pandas** - Data manipulation and cleaning
- **Jupyter Notebook** - Interactive development

## 📊 Key Statistics

### Price Distribution
- Median price: Check dataset for specific values
- Price range: $1,000 - $100,000,000+

### Property Characteristics
- Median bedrooms: 3.0
- Median bathrooms: 2.0
- Median house size: 1,760 sq ft
- Median lot size: 0.26 acres

## 🚀 How to Use This Dataset

### For Analysis (Python)
```python
import pandas as pd

# Load version with sale dates
df = pd.read_csv('housing_data_with_sold_date.csv')

# Basic info
print(df.info())
print(df.describe())

# Filter by city
houston_homes = df[df['city'] == 'Houston']
