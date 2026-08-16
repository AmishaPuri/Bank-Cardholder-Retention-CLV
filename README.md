# Bank Cardholder Retention & CLV Optimization via Survival Analysis

## Executive Summary
This project evaluates retail banking customer attrition ($N = 10,127$) using time-to-event statistical survival analysis. By replacing traditional binary classification with semi-parametric econometric modeling, this framework handles right-censored active accounts, quantifies risk drivers via hazard ratios, models 24-month discounted Customer Lifetime Value (CLV), and leverages GenAI to automate strategy briefs for executive leadership.

---

## Business Problem
In retail cardholder operations, traditional machine learning models treat active customers as static non-churners, ignoring tenure length and right-censoring. This leads to biased retention spend and poor allocation of marketing resources. 

The objectives of this project are:
1. Identify key operational and behavioral drivers of cardholder churn.
2. Estimate 24-month expected portfolio Customer Lifetime Value (CLV) using Net Present Value (NPV) cash flow discounting.
3. Compute 95% confidence intervals around portfolio CLV using non-parametric bootstrapping.
4. Integrate statistical parameters into a GenAI prompting pipeline for strategy generation.

---

## Methodology & Quantitative Framework

### 1. Non-Parametric Survival Analysis (Kaplan-Meier)
Estimated baseline customer retention probabilities over tenure ($T$) using the Kaplan-Meier estimator:
$$S(t) = \prod_{t_i \le t} \left(1 - \frac{d_i}{n_i}\right)$$
Evaluated statistical differences across demographic segments using non-parametric **Log-Rank Tests**.

### 2. Econometric Modeling (Cox Proportional Hazards)
Isolated individual risk factors by modeling the hazard rate $h(t | X)$:
$$h(t | X) = h_0(t) \exp\left(\sum_{i=1}^{p} \beta_i X_i\right)$$
Interpreted exponential coefficients $\exp(\beta_i)$ as **Hazard Ratios (HR)** to identify risk multipliers vs. protective factors.

### 3. Financial Cash Flow Discounting (CLV) & Bootstrapping
Combined expected survival probabilities $S(t)$ with net monthly customer margins $M$ at a 1% monthly financial discount rate ($r$):
$$\text{CLV} = \sum_{t=1}^{24} \frac{M \cdot S(t)}{(1 + r)^t}$$
Constructed a **1,000-sample non-parametric bootstrap** to calculate 95% confidence intervals for portfolio revenue.

### 4. GenAI Strategy Pipeline
Exported econometric summary parameters into a structured prompt framework to generate executive action plans.

---

## Key Results & Empirical Findings

| Metric / Analysis | Statistical Output | Business Interpretation |
| :--- | :--- | :--- |
| **Log-Rank Hypothesis Test** | $p = 0.0008$ | Statistically significant difference in survival curves across customer segments. |
| **Primary Churn Risk Factor** | $\text{HR} = 1.353$ ($p < 0.001$) | Each customer service contact increases instant churn risk by **35.3%**. |
| **Primary Retention Driver** | $\text{HR} = 0.808$ ($p < 0.001$) | Each additional bank product held reduces churn hazard by **19.2%**. |
| **Transaction Velocity** | $\text{HR} = 0.942$ ($p < 0.001$) | Higher transaction frequency shields accounts, cutting hazard by **5.8%** per transaction. |
| **Mean 24-Month Portfolio CLV** | **$581.87** | Discounted expected net financial value per account. |
| **95% Bootstrapped CI** | **[$576.76, $586.80]** | Empirical confidence bounds derived from 1,000 resamples. |

## Repository Structure

* `Bank_Customer_Survival_Analysis_CLV.ipynb` — Main Google Colab Notebook (Code, Outputs, Plots)
* `BankChurners.csv` — Core Dataset
* `churn_gender_logrank.png` — Kaplan-Meier Survival Curves
* `cox_hazard_ratios.png` — Hazard Ratio Plot with 95% CIs
* `executive_summary_prompt.txt` — Structured Econometric Input Brief for GenAI
* `README.md` — Project Summary

---

## Strategic Recommendations
1. **Support Call Intervention:** Re-engineer the customer service workflow for accounts reaching 3+ contacts to resolve operational friction before attrition occurs.
2. **Product Bundling Incentives:** Target single-product cardholders with multi-product rewards (e.g., savings accounts or credit lines) to lower hazard rates by ~19%.
3. **Engagement Campaigns:** Deploy targeted transaction incentives for accounts showing declining monthly card usage. rewards (e.g., savings accounts or credit lines) to lower hazard rates by ~19%.
## Repository Structure
