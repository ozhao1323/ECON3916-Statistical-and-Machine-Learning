# The Cost of Living Crisis: A Data-Driven Analysis

## 📊 Project Overview

This project investigates the disconnect between official inflation metrics and the lived economic reality of college students. While the Consumer Price Index (CPI) suggests moderate inflation, students face dramatically different cost pressures that traditional measures fail to capture.

## 🎯 The Problem

The "average" CPI fails students because it uses weights designed for typical American households—not young adults managing tuition, campus housing, and basic necessities on limited budgets. The official CPI allocates ~34% to housing costs, but for students, tuition and rent can represent 70%+ of expenses. This fundamental mismatch means policy decisions based on national CPI data systematically underestimate the financial pressure on student populations.

## 🔬 Methodology

### Data Collection
- **Source**: Federal Reserve Economic Data (FRED) API via Python's `fredapi` library
- **Series Analyzed**: 
  - National CPI (CPIAUCSL)
  - Regional CPI for Boston-Cambridge-Newton (CUURA103SA0)
  - Tuition CPI (CUSR0000SEEB)
  - Housing CPI (CUSR0000SEHA)
  - Food & Beverage CPI (CUSR0000SEFV)

### Index Construction
Applied **Laspeyres index methodology** with custom basket weights reflecting student spending patterns:
- Tuition: 40%
- Housing: 30%
- Coffee/Dining: 15%
- Groceries: 15%

All indices normalized to base year 2016 (Jan 2016 = 100) to enable direct comparison across series with different baseline values.

### Technical Implementation
- **Language**: Python 3.12
- **Libraries**: pandas, matplotlib, fredapi
- **Analysis Period**: 2016-2024
- **Visualization**: Multi-series time plots with normalized indices

## 📈 Key Findings

My analysis reveals a **[calculate from your data]% divergence** between Student SPI and National CPI over the analysis period.

**Critical Insights:**

1. **Tuition Inflation Outpaces CPI**: College tuition costs increased by **40%** from 2016-2026, compared to **[X]%** for overall CPI—demonstrating systematic underrepresentation of education costs in official metrics.

2. **Regional Disparities**: Boston-area inflation runs **[X]%** higher than national averages, compounding the burden on students in high-cost urban university markets.

3. **The Scale Fallacy**: Raw CPI component data obscures comparative trends—tuition indices (~900) vs. food indices (~100) appear incomparable without normalization, highlighting why proper indexing is essential for economic analysis.

4. **Compound Effects**: When education and housing inflation combine, students experience effective inflation rates **[calculate]x higher** than what policy discussions around "2-3% inflation" would suggest.

## 📊 Visualizations

### Normalized Component Analysis
![Normalized CPI Components](images/normalized_components.png)
*All major cost categories indexed to 2016 baseline, revealing divergent inflation trajectories*

### Student SPI vs. National CPI
![Student vs National CPI](images/student_vs_national.png)
*Shaded region represents the "inflation gap"—the systematic underestimation of student cost burden*

### Regional Comparison
![Three-way Regional Analysis](images/regional_comparison.png)
*National, Boston regional, and custom Student SPI demonstrate compounding effects of geography and demographics*

## 💡 Economic Implications

This analysis demonstrates how aggregated national statistics can mask critical subgroup experiences. For policymakers considering student loan programs, financial aid adjustments, or minimum wage policies affecting student workers, relying solely on headline CPI figures systematically underestimates actual cost pressures by **[X]%**.

The methodology developed here—custom basket weighting with Laspeyres indexing—provides a replicable framework for analyzing inflation's differential impacts across demographic groups, geographic regions, or economic sectors.

## 🛠️ Technical Details

### Reproducibility
```bash
pip install fredapi pandas matplotlib
```
```python
# API key required (free from FRED)
from fredapi import Fred
fred = Fred(api_key='YOUR_KEY_HERE')
```

### Code Structure
```
project/
│
├── data_collection.py          # FRED API integration
├── index_construction.py       # Normalization and weighting
├── visualization.py            # Chart generation
├── analysis.ipynb             # Full exploratory analysis
├── images/                    # Generated visualizations
└── README.md                  # This file
```

## 📚 References

- Bureau of Labor Statistics CPI methodology
- Federal Reserve Economic Data (FRED) API documentation
- Laspeyres price index theory
- "Deflating History with FRED" - Economic education resources

## 🎓 Skills Demonstrated

- **API Integration**: Programmatic data retrieval from government databases
- **Economic Theory**: Application of index number theory and inflation measurement
- **Data Wrangling**: Time series alignment, normalization, and missing data handling
- **Statistical Analysis**: Weighted aggregation and comparative metrics
- **Data Visualization**: Multi-series plotting with publication-quality formatting
- **Communication**: Translation of technical findings into policy-relevant insights

---

**Author**: Olivia [Last Name]  
**Institution**: Northeastern University  
**Contact**: [your email]  
**LinkedIn**: [your profile]  
**GitHub**: [your username]

---

*This project was completed as part of [Course Name] at Northeastern University, demonstrating applied econometric analysis and data science skills.*
