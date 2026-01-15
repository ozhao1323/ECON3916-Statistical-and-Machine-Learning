## Lab 2: The Illusion of Growth & The Composition Effect

### 🎯 Objective

Build a Python pipeline to ingest live economic data from the Federal Reserve API (FRED) to analyze wage stagnation in the United States and correct for statistical biases that distort our understanding of labor market dynamics.

### 🔬 Methodology

**Tech Stack:** Python, `fredapi`, `pandas`, `matplotlib`

#### Data Acquisition & Processing
1. **API Integration**: Connected to the Federal Reserve Economic Data (FRED) API to fetch real-time macroeconomic series:
   - `AHETPI`: Average Hourly Earnings of Production Workers (Nominal Wages)
   - `CPIAUCSL`: Consumer Price Index for All Urban Consumers (Inflation Measure)
   - `ECIWAG`: Employment Cost Index for Wages and Salaries (Composition-Controlled Measure)

2. **Real Wage Calculation**: Deflated nominal wages using CPI to compute real purchasing power over a 50+ year period (1964-Present), revealing the true trajectory of worker compensation adjusted for inflation.

3. **Anomaly Detection**: Identified a sharp statistical spike in 2020 average wages during the COVID-19 pandemic—a counterintuitive result given widespread economic disruption.

4. **Bias Correction**: Applied the Employment Cost Index (ECI) to control for the **Composition Effect**—a statistical bias that occurs when the mix of workers in the labor force changes. By holding workforce composition constant, the ECI reveals whether wage changes reflect genuine increases in compensation versus shifts in who remains employed.

### 📊 Key Findings

#### The Money Illusion (1964-Present)
Visualization revealed that while nominal wages have grown steadily over five decades, **real wages have remained essentially flat** when adjusted for inflation. This demonstrates the "money illusion"—workers earn more dollars but have similar purchasing power to their counterparts 50 years ago.

#### The Pandemic Paradox (2020 Composition Effect)
The 2020 wage data showed an artificial spike in standard average wage metrics, creating the misleading impression of a pandemic wage boom. However, comparison with the Employment Cost Index proved this was a **statistical artifact**, not a real economic phenomenon:

- **Standard Average Wages**: Showed sharp upward spike in 2020
- **Employment Cost Index**: Demonstrated stable, modest growth through the same period

**Root Cause**: Low-wage workers disproportionately exited the labor force during pandemic lockdowns (restaurants, retail, hospitality). When these workers left the sample, the remaining workforce had a higher average wage—not because anyone got a raise, but because the denominator changed. This is the **Composition Effect** in action.

**Economic Insight**: The 2020 "wage growth" reflected labor force contraction among low-wage workers, not increased labor demand or genuine wage gains. This highlights the critical importance of using composition-adjusted metrics (like the ECI) when analyzing labor market trends during periods of structural economic disruption.

---

**Takeaway**: This project demonstrates how raw economic statistics can be misleading without proper adjustment for underlying compositional changes, and showcases the power of programmatic API access for real-time economic analysis.
