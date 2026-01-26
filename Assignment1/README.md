# The Cost of Living Crisis: A Data-Driven Analysis

A Python-based analysis revealing how official inflation metrics fail to capture the true cost increases faced by college students.

## 📊 Project Overview

This project constructs a custom "Student Price Index" (SPI) to demonstrate the significant divergence between official Consumer Price Index (CPI) measurements and the actual inflation experienced by college students. Through data analysis of Federal Reserve Economic Data (FRED), this study quantifies the hidden financial burden facing students today.

## 🎯 The Problem

The official Consumer Price Index (CPI) serves as the standard measure of inflation in the United States. However, this "average" metric obscures a critical reality: college students experience vastly different rates of price increases compared to the general population.

**Key Issues:**
- Students allocate budgets differently than average households
- Official CPI includes items irrelevant to students (healthcare, home furnishings, vehicles)
- Student-specific expenses (tuition, rent, food) are underweighted in official metrics
- Policy decisions based on official CPI fail to address student financial pressure

## 🔬 Methodology

### Data Sources
This analysis leverages the Federal Reserve Economic Data (FRED) API to retrieve official CPI data across multiple consumption categories:

- **Tuition** (`CUSR0000SEEB`)
- **Rent** (`CUSR0000SEHA`)
- **Food Away from Home** (`CUSR0000SEFV`) - proxy for dining expenses
- **Streaming Services** (`CUSR0000SERA02`)
- **Official CPI** (`CPIAUCSL`)

### Technical Approach

**Normalization Formula:**
```
Value_Index = (Value_Current / Value_at_Start_Date) × 100
```

All indices were normalized to January 2016 = 100. This normalization is critical because raw CPI data uses different base years (e.g., 1982 for tuition, 2002 for streaming), making direct comparison impossible without re-indexing.

**Theoretical Foundation:**  
The analysis follows the Laspeyres price index methodology, which measures how the cost of a fixed basket of goods changes over time, isolating pure price effects from consumption changes.

### Tools & Technologies
- **Python 3.x**
- **fredapi** - Federal Reserve Economic Data API
- **pandas** - Data manipulation and analysis
- **matplotlib** - Data visualization

## 📈 Key Findings

### 1. The Data Crime: Raw vs. Normalized Data

Raw CPI values are misleading when compared directly:
- Tuition (Raw): ~900
- Streaming (Raw): ~600

This suggests tuition is only 50% higher than streaming, but these numbers use different base years and cannot be compared meaningfully.

### 2. Student Inflation Exceeds Official Measures

After proper normalization (2016 = 100):

| Category | 2026 Index | Inflation Rate |
|----------|------------|----------------|
| **Official CPI** | ~137 | **37%** |
| **Rent** | ~151 | **51%** |
| **Food/Burritos** | ~150 | **50%** |
| **Streaming** | ~141 | **41%** |
| **Tuition** | ~129 | **29%** |

### 3. The Student Inflation Gap

**Most student expenses have experienced inflation rates 35-40% higher than the official CPI.** This divergence represents a hidden financial burden not captured in policy discussions or financial aid calculations.

### 4. Policy Implications

- **Financial Aid Erosion**: Federal aid tied to official CPI underestimates actual student needs
- **Minimum Wage Inadequacy**: Wage adjustments based on national CPI don't keep pace with student living costs
- **Invisible Crisis**: Students face financial pressures hidden in headline inflation numbers

## 🖼️ Visualizations

### Raw Data Comparison (The "Bad" Chart)
Demonstrates why comparing indices with different base years is misleading.

### Normalized Price Trends (2016 = 100)
Shows true comparative growth rates across all student expense categories vs. official CPI.

## 💻 Installation & Usage

### Prerequisites
```bash
pip install fredapi pandas matplotlib
```

### Setup
1. Obtain a FRED API key from https://fred.stlouisfed.org/docs/api/api_key.html
2. Clone this repository
3. Replace `your_api_key_here` in the code with your actual FRED API key

### Running the Analysis
```python
python student_inflation_analysis.py
```

## 📁 Project Structure
```
├── student_inflation_analysis.py   # Main analysis script
├── README.md                        # Project documentation
├── images/
│   ├── raw_cpi_comparison.png     # Raw data visualization
│   └── normalized_trends.png       # Normalized comparison
└── requirements.txt                 # Python dependencies
```

## 🎓 Skills Demonstrated

- **Python Programming**: API integration, data manipulation, automation
- **Data Science**: Time series analysis, normalization techniques, index construction
- **Statistical Methods**: Laspeyres price index methodology, economic analysis
- **Data Visualization**: Clear, professional matplotlib charts
- **Economic Analysis**: Understanding of CPI methodology and limitations
- **Technical Communication**: Translating complex analysis into actionable insights

## 🔍 Conclusion

The official CPI accurately measures inflation for the average American household, but it's fundamentally inadequate for understanding the student experience. This analysis quantifies what students know intuitively: **their cost of living is rising far faster than national averages suggest.**

By constructing a student-specific price index using rigorous data science methods, this project demonstrates:
- The importance of demographic-specific economic metrics
- Critical limitations of one-size-fits-all inflation measurements
- The power of custom index construction for policy analysis

For policymakers, university administrators, and students, understanding this divergence is essential for addressing the true scope of college affordability challenges.

## 📧 Contact

**Sebastian Romero**  
Data Science & Economics Student | Northeastern University  
Head of Marketing, Kaleidoscope

[LinkedIn](#) | [GitHub](#) | [Email](mailto:your.email@northeastern.edu)

---

*This project was completed as part of a data science portfolio demonstrating practical applications of economic analysis and Python programming.*
