# Air Quality Analysis — India (2015–2020)
### Statistical Study of PM2.5 Pollution Patterns Across Indian Cities

---

## Objective

To perform exploratory data analysis and statistical inference on India's air quality data — studying pollutant distributions, seasonal pollution patterns, city-level comparisons, and hypothesis testing on PM2.5 concentration across seasons.

This project applies distribution fitting, correlation analysis, and statistical testing to understand the underlying structure of air pollution data in Indian cities from 2015 to 2020.

---

## Dataset

**India Air Quality Data (city_day.csv)** — sourced from Kaggle

- **29,531 daily observations** across multiple Indian cities
- **16 features** — City, Date, PM2.5, PM10, NO, NO2, NOx, NH3, CO, SO2, O3, Benzene, Toluene, Xylene, AQI, AQI_Bucket
- Covers years **2015 to 2020**
- 13 numeric pollutant columns + 3 categorical columns (City, Date, AQI_Bucket)

---

## Tools & Libraries

| Tool | Purpose |
|---|---|
| Python | Core language |
| Pandas | Data loading and manipulation |
| NumPy | Numerical computations |
| Matplotlib & Seaborn | Visualizations |
| Scipy (stats) | Distribution fitting, T-test |

---

## Project Structure

```
Air-Quality_Project.ipynb    ← Main analysis notebook
datasets/
  city_day.csv               ← Dataset (from Kaggle)
README_AirQuality.md         ← This file
```

---

## Key Results

### 1. Dataset Overview

- **Total rows:** 29,531 daily city-level observations
- **Total columns:** 16 (after feature engineering: 19)
- **No missing values** in City and Date columns
- All pollutant columns have missing data to varying degrees

### 2. Missing Values Summary

| Column | Missing Values | % Missing |
|---|---|---|
| Xylene | 18,109 | 61.3% — most missing |
| NH3 | 10,328 | 35.0% |
| PM10 | 11,140 | 37.7% |
| Toluene | 8,041 | 27.2% |
| Benzene | 5,623 | 19.0% |
| AQI / AQI_Bucket | 4,681 | 15.9% |
| PM2.5 | 4,598 | 15.6% |
| CO | 2,059 | 7.0% — least missing |

> **Imputation Strategy:** PM2.5 and PM10 were filled using **median** (not mean) because both columns are right-skewed — median is more robust to outliers in skewed data.

### 3. Statistical Summary (Key Pollutants)

| Pollutant | Mean | Median | Observation |
|---|---|---|---|
| PM2.5 | 67.45 µg/m³ | 48.57 µg/m³ | Right-skewed |
| PM10 | 118.13 µg/m³ | 95.68 µg/m³ | Right-skewed |
| AQI | 166.46 | 118.00 | Heavily right-skewed |
| Toluene | 8.70 | 2.97 | Very right-skewed |

> Almost all pollutant columns are right-skewed — extreme pollution spike events pull the mean well above the median.

### 4. Distribution Fitting on PM2.5

Two distributions were fitted to PM2.5 data and compared visually:

| Distribution | Observation |
|---|---|
| Exponential (Red curve) | Overestimates low values, poor tail fit |
| **Log-Normal (Green curve)** | **Better fit — matches the right-skewed shape of PM2.5** |

**Conclusion:** Log-Normal distribution fits PM2.5 data better than Exponential — consistent with environmental science literature on pollutant concentration distributions.

### 5. Yearly Trend (2015–2020)

| Year | Avg PM2.5 (µg/m³) |
|---|---|
| 2015 | ~72 |
| 2016 | ~82 (Peak) |
| 2017 | ~75 |
| 2018 | ~66 |
| 2019 | ~59 |
| 2020 | ~44 (Lowest) |

> **Observation:** PM2.5 shows a clear **declining trend from 2016 to 2020**. The sharp drop in 2020 is likely attributable to reduced industrial activity and vehicular movement during the COVID-19 lockdown.

### 6. Monthly Seasonality

| Season | Avg PM2.5 Pattern |
|---|---|
| November | ~104 µg/m³ — Highest |
| December | ~102 µg/m³ |
| January | ~97 µg/m³ |
| July–August | ~37–40 µg/m³ — Lowest |

> **Observation:** PM2.5 peaks sharply in winter months (Nov–Jan) and drops to its lowest in monsoon months (Jul–Aug). This is consistent with reduced wind dispersion, temperature inversions, and increased biomass burning in winter.

### 7. Seasonal Boxplot (PM2.5 Distribution by Season)

| Season | Pattern |
|---|---|
| Winter | Highest median PM2.5; many high outliers |
| Spring | Moderate; wide spread |
| Summer | Lowest median; some extreme outliers |
| Autumn | Moderate; wide spread with many outliers |

> Winter shows the widest interquartile range, indicating highly variable pollution levels — some days are extreme, some are moderate, depending on wind conditions.

### 8. Top 10 Most Polluted Cities (Average PM2.5)

| Rank | City | Avg PM2.5 |
|---|---|---|
| 1 | Delhi | ~118 µg/m³ |
| 2 | Gurugram | ~112 µg/m³ |
| 3 | Patna | ~111 µg/m³ |
| 4 | Lucknow | ~109 µg/m³ |
| 5 | Guwahati | ~63 µg/m³ |
| 6 | Kolkata | ~62 µg/m³ |
| 7 | Ahmedabad | ~61 µg/m³ |
| 8 | Brajrajnagar | ~61 µg/m³ |
| 9 | Talcher | ~59 µg/m³ |
| 10 | Amritsar | ~53 µg/m³ |

> Delhi and surrounding NCR cities (Gurugram, Lucknow) dominate the top rankings — consistent with high vehicular density, industrial activity, and stubble burning in the Indo-Gangetic Plain.

### 9. Correlation Matrix (Key Pollutants)

| Pollutant Pair | Correlation | Interpretation |
|---|---|---|
| PM2.5 ↔ PM10 | **0.52** | Moderate positive — common particulate sources |
| NO ↔ NOx | **0.79** | Strong positive — NOx is largely composed of NO |
| NO2 ↔ NOx | **0.63** | Strong positive — both vehicular/combustion origin |
| PM2.5 ↔ CO | 0.09 | Weak — different emission pathways |

> **Observation:** PM2.5 and PM10 show moderate positive correlation (0.52), suggesting common emission sources such as vehicular exhaust and industrial dust. NO and NOx show strong correlation (0.79) as expected — NOx is chemically defined as NO + NO2.

### 10. Hypothesis Testing — Winter vs Summer PM2.5

**Test: Independent T-Test**
> H₀: Mean PM2.5 in Winter = Mean PM2.5 in Summer
> H₁: Mean PM2.5 in Winter > Mean PM2.5 in Summer

| Metric | Value |
|---|---|
| Winter Mean PM2.5 | **92.14 µg/m³** |
| Summer Mean PM2.5 | **40.49 µg/m³** |
| T-statistic | **54.8570** |
| P-value | **< 0.000001** |
| Result | ✅ **Statistically significant difference** |

> **Conclusion:** Winter PM2.5 is more than **2.27× higher** than Summer PM2.5. The T-statistic of 54.86 and p-value of essentially zero confirms this is not due to random chance — seasonal variation is a real, significant driver of PM2.5 levels in India.

---

## Key Findings & Conclusions

1. **Log-Normal distribution** fits PM2.5 data better than Exponential — consistent with environmental data literature on right-skewed pollutant concentrations.

2. **PM2.5 peaked in 2016 (~82 µg/m³) and declined steadily to ~44 µg/m³ in 2020**, with the 2020 drop likely driven by COVID-19 lockdown restrictions.

3. **Strong seasonal pattern** — Winter PM2.5 (92.14 µg/m³) is more than double Summer PM2.5 (40.49 µg/m³), confirmed statistically by T-test (p < 0.05).

4. **Delhi, Gurugram, and Patna are consistently the most polluted cities**, all exceeding 100 µg/m³ average PM2.5 — well above the WHO safe limit of 15 µg/m³.

5. **NO and NOx show strong correlation (0.79)**, confirming vehicular combustion as the dominant source of nitrogen oxides. PM2.5 and PM10 correlation (0.52) suggests shared particulate emission sources.

6. **Xylene (61% missing) and NH3 (35% missing)** are the most data-sparse pollutants — caution should be exercised in any modelling involving these columns.

---

## Future Scope

- Time series forecasting of PM2.5 using ARIMA / SARIMA models
- Spatiotemporal modelling across cities (as in Kayal et al., 2024)
- Survival analysis on "days exceeding WHO safe limit" (PM2.5 > 15 µg/m³)
- Clustering cities by pollution profile using K-Means
- AQI prediction using regression models

---

## Dataset Source

India Air Quality Data — city_day.csv  
Available on Kaggle: https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india
