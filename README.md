# 📉 Optimizing E-Commerce Conversion: A/B Test Analysis

![Python](https://img.shields.io/badge/Python-3.9-blue)
![Status](https://img.shields.io/badge/Status-Complete-green)
![Library](https://img.shields.io/badge/Library-Statsmodels-orange)

## 📌 Executive Summary
**Objective:** Determine if a new landing page design increases user conversion rates compared to the current "control" page.
**Method:** Randomized Controlled Trial (A/B Test) on 290,000+ user sessions.
**Result:** The experiment **failed to reject the null hypothesis** ($p = 0.19$). The new page actually performed slightly worse (11.88%) than the control (12.04%).
**Recommendation:** **Do not launch.** Retain the original page to avoid potential revenue loss and engineering debt.

---

## 📖 Project Background
An e-commerce platform developed a new landing page with the hypothesis that it would improve the conversion rate (currently ~12%). Before a full rollout, we ran an A/B test to validate this claim statistically.

* **Metric:** Conversion Rate (Unique "converted" users / Total unique users)
* **Statistical Test:** Two-proportion Z-test
* **Significance Level ($\alpha$):** 0.05
* **Target Power ($1-\beta$):** 0.80

---

## 🛠️ Technical Stack
* **Language:** Python
* **Libraries:** `pandas`, `numpy`, `scipy`, `statsmodels`, `matplotlib`, `seaborn`
* **Environment:** PyCharm / Jupyter Notebook

---

## 📊 Experimental Design & Data Cleaning

### 1. Power Analysis
Before analyzing the data, I performed a Power Analysis to determine the minimum sample size required to detect a **2% lift** (from 12% to 14%) with 80% power.
* **Required Sample Size:** ~4,400 users per group.
* **Actual Sample Size:** ~145,000 users per group (Test is highly powered).

### 2. Data Quality Checks
Real-world data is messy. I implemented strict data cleaning protocols:
* **Mismatch Removal:** Removed 3,893 rows where the `group` (instruction) did not match the `landing_page` (reality).
* **Duplicate Removal:** Dropped users who appeared multiple times to ensure independence of observations.
* **SRM Check:** Verified the randomization algorithm using a **Sample Ratio Mismatch (SRM)** test.
    * Result: 49.99% Control / 50.01% Treatment (Perfect Split).

---

## 📈 Analysis & Results

### Conversion Rates
| Group | Conversion Rate | Standard Deviation | Sample Size |
| :--- | :--- | :--- | :--- |
| **Control** | 12.04% | 0.325 | 145,274 |
| **Treatment** | 11.88% | 0.323 | 145,310 |

*Observation: The Treatment group conversion rate is slightly lower than the Control.*

### Statistical Inference (Z-Test)
* **Z-Statistic:** 1.31
* **P-Value:** 0.1899
* **Confidence Intervals (95%):**
    * Control: [11.87%, 12.21%]
    * Treatment: [11.71%, 12.05%]

### Interpretation
Since the p-value (0.19) is greater than our alpha (0.05), the difference is **not statistically significant**. Furthermore, the Confidence Intervals overlap significantly, confirming that we cannot distinguish the new page's performance from the old one.

---

## 💡 Business Recommendation
Based on the data, the new design **did not drive the intended behavior change**.

1.  **Stop the Launch:** Deploying the new page introduces risk without proven benefit.
2.  **Investigate:** The new page performed slightly worse. I recommend conducting qualitative user research (heatmaps, user surveys) to understand *why* the new design caused friction.
3.  **Iterate:** Use these findings to design a new variation and run a follow-up test.

---

## 📂 Repository Structure
```text
├── data/
│   └── ab_data.csv          # Raw dataset (GitIgnore if large)
├── notebooks/
│   ├── 01_Experiment_Design.ipynb    # Power Analysis & Cleaning
│   └── 02_Statistical_Analysis.ipynb # Z-Test & Visualization
├── src/
│   └── plots.py             # Custom plotting functions
├── README.md                # Project Overview
└── requirements.txt         # Dependencies
