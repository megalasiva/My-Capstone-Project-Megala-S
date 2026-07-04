# My Capstone Project - Part 1 

This repository contains the data extraction, cleaning pipeline, and Exploratory Data Analysis (EDA) for Part 1 of the Capstone project. 

---

## 1. Data Cleaning & Handling Missing Values
- **Duplicates:** During data extraction, 12 duplicate rows were found in the dataset. I removed them immediately using pandas `.drop_duplicates()` to avoid data leakage before any modeling takes place.
- **Missing Values:** There were minor missing values in the `RSI_14D` column (around 0.58%). I used **Median Imputation** to fill these blanks. I chose the median because financial metrics are often skewed by massive market events, and using the mean would pull our filled values away from the true center.
- **Optimization:** To save memory, I explicitly changed the `Asset_Class` column from a regular text string to a Pandas `category` type.

---

## 2. Asymmetry & Outlier Analysis
- **Skewness:** The `Trading_Volume` column showed an extremely high positive skewness score. This is normal for financial markets because most trading days have a steady, average volume, while a few major news days cause massive volume spikes.
- **Outliers:** I used the Interquartile Range (IQR) method on the `Daily_Return` column to discover extreme market outliers. I chose **not** to remove these outliers because extreme daily price jumps are completely genuine market events. If we delete them, our future machine learning models won't learn how to handle real market risks.

---

## 3. Pearson vs. Spearman Insight
- When analyzing the correlations between columns, I noticed a clear difference between the Pearson and Spearman scores. 
- Pearson only tracks straight-line relationships, while Spearman catches ranked, non-linear trends. The divergence between them proofs that the features in this dataset connect in non-linear ways. 
- Because of this, standard linear regression models will likely struggle. Moving into Part 2, I will prioritize non-linear tree algorithms like **Random Forest** or **Gradient Boosting** to capture these complex market patterns.
