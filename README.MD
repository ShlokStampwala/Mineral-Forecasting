# ⛏️ AI-Driven Strategic Mineral Forecasting & Risk Analysis

![Status](https://img.shields.io/badge/Status-Completed-success)
![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![ML](https://img.shields.io/badge/Machine%20Learning-Scikit--Learn-orange)
![Focus](https://img.shields.io/badge/Minerals-Copper%20|%20Lithium%20|%20Graphite-black)

## 📌 Executive Summary
India's "Atmanirbhar Bharat" (Self-Reliant India) initiative faces a strategic challenge: heavy dependency on imports for critical minerals like **Copper, Lithium, and Graphite**. 

This project moves beyond static trend analysis. We utilized **Machine Learning with Automated Hyperparameter Tuning** to analyze historical trade data (2018-2024) and forecast the demand curve for 2025-2026. The system automatically identifies whether demand is growing linearly, accelerating (curved), or stabilizing.

---
## For Dashboard Check This Link please:-
[Dashboard Github Link](https://github.com/ShlokStampwala/Mineral-Forecasting_Working_MVP.git)

## 🚀 Key Innovation: The "Champion Model" Selector
Unlike traditional forecasting which uses a single method, our algorithm runs a **"Battle of Models"** for every mineral:

1.  **Linear Regression:** Tests for steady, straight-line growth.
2.  **Polynomial Regression (Degree 2):** Tests for accelerating/curved growth.
3.  **Exponential Smoothing (Holt’s):** Tests for time-weighted trends.

**The system automatically selects the model with the Lowest RMSE (Error Score) to generate the final forecast.**

---
# 🧠 Technical Deep Dive: Statistical Models Explained

This document explains the mathematical logic behind the **Forecasting (ARIMA/Regression)** and **Dependency Analysis (ANOVA)** used in this project.

---

## 1. The Forecasting Engine: Why "Battle of Models"?

In time-series forecasting, no single model is perfect for every type of data. Our project initially considered **ARIMA (AutoRegressive Integrated Moving Average)** but evolved into a **Dynamic Model Selection System**.

### 📉 What is the challenge?
* **Data Scarcity:** We have annual data from 2018-2024 (7 data points).
* **ARIMA's Limitation:** Standard ARIMA models typically require 30+ data points to be statistically robust. Using them on small datasets often results in flat-line predictions.

### 🚀 Our Solution: The "Champion Model" Approach
Instead of forcing ARIMA, we implemented an algorithm that trains **three distinct mathematical models** and picks the winner based on the lowest Error Rate (RMSE).

#### A. Linear Regression (The "Steady" Model)
* **Math:** $y = mx + c$
* **Role:** Assumes demand grows at a constant rate.
* **Where it won:** **Graphite**. Since Graphite demand is mature and stable, a straight line provided the most accurate forecast without overcomplicating the data.

#### B. Polynomial Regression (The "Curve" Model)
* **Math:** $y = \beta_0 + \beta_1x + \beta_2x^2 + ...$
* **Role:** Captures **non-linear acceleration**. It allows the forecast line to "bend" upwards.
* **Where it won:** **Copper & Lithium**.
    * **Why?** The data showed a "Hockey Stick" pattern (slow start, then rapid rise). A simple straight line (Linear) or mean-reverting model (ARIMA) would have *underestimated* the explosion in demand caused by the EV sector.

#### C. Exponential Smoothing (Holt’s Method)
* **Role:** A weighted forecasting method where recent years (2023-24) are given more "importance" (weight) than older years (2018).
* **Usage:** Used as a validator to cross-check trends.

---

## 2. Dependency Risk Analysis: The Role of ANOVA

While Forecasting tells us *how much* we need, **ANOVA (Analysis of Variance)** tells us *how risky* our supply chain is.

### 🧪 What does ANOVA do?
ANOVA is a statistical test used to determine if there are **statistically significant differences** between the means of three or more independent groups.

### 🎯 Application in this Project:
We applied logic similar to ANOVA to analyze **Import Origins** (Country-wise Data).

* **Hypothesis:** "Is India's import dependency distributed evenly among countries, or is it significantly skewed towards one?"
* **The Test:** We compared the variance of import volumes from different trade partners (e.g., China vs. Chile vs. Indonesia).
* **The Result:**
    * **High Variance (Significant p-value):** Indicates that one country (e.g., China for Graphite) dominates the supply. This mathematically proves **"High Strategic Risk."**
    * **Low Variance:** Indicates a diversified supply chain (Imports spread across multiple nations).

---

## 3. Performance Metric: RMSE (Root Mean Squared Error)

To eliminate human bias in model selection, we used **RMSE** as the referee.

$$RMSE = \sqrt{\frac{1}{n}\Sigma_{i=1}^{n}{\Big(\frac{d_i -f_i}{\sigma_i}\Big)^2}}$$

* **Logic:** It measures the "distance" between the Model's predicted line and the Actual historical dots.
* **Result:**
    * Lower RMSE = The model explains the reality better.
    * **Example:** For Copper, the Linear model had an error of ~8,000. The Polynomial model had an error of ~5,600. The system automatically discarded Linear and chose Polynomial.

---

## 4. Summary: The "So What?"

| Method | Technical Purpose | Business Value (What we tell the Govt) |
| :--- | :--- | :--- |
| **Polynomial Regression** | Fits a curved line to data | "Demand for Lithium is not just growing; it is **exploding** exponentially." |
| **Linear Regression** | Fits a straight line | "Graphite demand is predictable and stable." |
| **ANOVA / Variance** | Measures spread of data | "Our reliance on a single country for Copper is mathematically **dangerous**." |