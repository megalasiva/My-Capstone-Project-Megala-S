# My Capstone Project - Part 2 

This folder contains the predictive models, trained algorithms, performance evaluation metrics, and sensitivity analysis for Part 2 of the Capstone project.

---

## 1. Class Imbalance Check
- Before modeling, the label distribution for `y_clf` was verified using `.value_counts()`. Because the classification targets were explicitly binarized relative to the dataset's median daily return, the classes are perfectly balanced (50% split). 
- Since neither class dropped below the 35% threshold, no synthetic rebalancing (such as SMOTE) or handling via class weights was necessary.

---

## 2. Regression vs. Classification Performance
- **Regression Analysis:** Both OLS Linear Regression and Ridge Regression yielded identical performance ($MSE = 0.000675$, $R^2 = 0.0016$). The near-zero $R^2$ indicates that linear models cannot effectively capture daily market price changes, as financial returns are heavily non-linear and subject to noise. 
- **Classification Analysis:** The Baseline Logistic Regression ($C=1.0$) achieved an Accuracy of 49.66%, Precision of 50.68%, Recall of 49.34%, and an F1-Score of 0.5000. This mirrors the ROC output where the $AUC = 0.49$. An AUC near 0.50 confirms that the linear classification boundary performs equivalent to random guessing on this market trend data.

---

## 3. Formulas & Metric Definitions
- **Precision:** $\text{Precision} = \frac{TP}{TP + FP}$
  - Measures the accuracy of positive predictions. If false positives are highly costly (e.g., executing a bad buy trade), we must optimize for high precision.
- **Recall:** $\text{Recall} = \frac{TP}{TP + FN}$
  - Measures the percentage of actual positive instances captured. If missing out on a market trend is more costly (omission risk), we must optimize for high recall.

---

## 4. Threshold Sensitivity & Regularization Analysis
- **Threshold Variations:**
  - Lowering the decision threshold to `0.3` pushes Recall to a perfect `1.000` but drops precision down, whereas raising it to `0.7` completely suppresses predictions. The threshold maximizing the F1-score on this dataset is **0.3** ($\text{F1} = 0.676$).
- **Regularization Experiment ($C=0.01$):**
  - Tightening the L2 penalty ($C=0.01$) resulted in a 95% Bootstrap Confidence Interval for the AUC difference of **[-0.027130, 0.002149]**. Because this interval contains exactly 0, we conclude there is no statistically significant performance variance between the baseline and strongly regularized models.
