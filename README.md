# A/B Testing: E-Commerce Landing Page Optimization

## 📌 Executive Summary
**Goal:** Determine if a new landing page design increases user conversion rates.
**Result:** The experiment **failed to reject the null hypothesis**. The new design did not show a statistically significant improvement.
**Recommendation:** Do not launch the new page. Maintain the current control version to avoid potential revenue loss.

## 📊 Project Background
An e-commerce platform developed a new landing page with the hypothesis that it would improve the conversion rate (currently ~12%). We ran a randomized controlled experiment (A/B Test) to validate this claim.

* **Metric:** Conversion Rate (Unique "converted" users / Total unique users)
* **Method:** Two-sample Z-test for proportions
* **Significance Level ($\alpha$):** 0.05
* **Power:** 0.80

## 🛠️ Tech Stack
* **Language:** Python 3.9
* **Libraries:** Pandas, Numpy, Scipy, Statsmodels, Matplotlib
* **Environment:** PyCharm + Jupyter Notebook

## 📈 Experimental Design
Before running the test, I performed a Power Analysis to determine the required sample size.
* **Baseline Conversion:** 12%
* **Minimum Detectable Effect (MDE):** 2%
* **Required Sample Size:** ~4,400 users per group

The actual dataset contained over **290,000 users**, providing ample statistical power to detect even small differences.

## 🔍 Analysis & Results
After cleaning the data (removing 3,893 users with mismatched group/page assignment), I verified the integrity of the randomization (Sample Ratio Mismatch check passed with a 50/50 split).

| Group | Conversion Rate | Sample Size |
| :--- | :--- | :--- |
| **Control** | 12.04% | 145,274 |
| **Treatment** | 11.89% | 145,310 |

### Statistical Test
* **Z-Statistic:** 1.24
* **P-Value:** 0.216

## 💡 Conclusion
With a p-value of **0.216**, we do not have sufficient evidence to reject the null hypothesis. The observed difference (Treatment performing slightly worse) is likely due to random chance or the new design potentially being less effective. 

**Business Recommendation:** Stick with the original landing page.