# 🔍 Housing Market Outlier Analysis: Comparative Forensics

Statistical framework comparing normal market behavior vs. outliers in California housing data using robust statistics and the **Inequality Wedge** metric.

## 🎯 Goal
Quantify distributional differences between core market and outliers using central tendency, volatility, and skewness measures.

## 📊 Methodology
- **Data Split**: Normal vs. Outlier populations (Isolation Forest detection)
- **Metrics**: Mean, Median, Std Dev, MAD (Median Absolute Deviation)
- **Key Variables**: `MedInc` (income), `MedHouseVal` (house value)
- **Inequality Wedge**: Mean - Median (quantifies right-skewness)

## 📈 Key Findings
- **Positive Inequality Wedge** in outliers → High-end concentration (Pareto dynamics)
- **Higher Std/MAD ratio** in outliers → Extreme values dominate traditional volatility
- **Visual Analysis**: Core market (symmetric) vs. Tail (extended, skewed)

## 💡 Insights
1. Outliers represent distinct market segment with fundamentally different characteristics
2. Traditional volatility measures (Std Dev) overstate risk in outlier segments
3. Evidence of wealth concentration consistent with 80/20 rule

## 🛠️ Tech Stack
```bash
pip install pandas numpy matplotlib scipy
```
Python, Pandas, Matplotlib, SciPy (MAD calculation)

## 🚀 Usage
```python
python comparative_forensics.py
```
Generates: Statistical tables, inequality wedge metrics, side-by-side histograms

## 📁 Structure
```
├── comparative_forensics.py    # Main analysis
├── README.md
├── requirements.txt
└── outputs/
    └── pareto_visualization.png
```

## 🔬 MAD vs Std Dev
- **Std Dev**: Sensitive to outliers, use for normal distributions
- **MAD**: Robust alternative for heavy-tailed data
- **Ratio**: Indicates outlier influence level

## 🔮 Future Work
- Time-series outlier evolution
- Geographic clustering analysis
- Separate ML models per population
- Causal inference on outlier predictors

## 📧 Contact
**Olivia** | Northeastern University CS  
Questions? Open an issue

## 📄 License
MIT License

---
**Built with 🔍 for understanding Pareto dynamics in real estate markets**
