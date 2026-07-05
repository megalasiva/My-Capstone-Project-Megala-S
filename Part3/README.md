# My Capstone Project - Part 3 

This folder details the configuration, evaluation metrics, and low-dimensional segment profiling for the Unsupervised Learning component of the Capstone project.

---

## 1. Optimal Cluster Determination
- **Elbow Curve Analysis:** The point where the deceleration curve begins to stabilize indicates our optimal cluster boundary. Based on the calculated Inertia drop-off, $K=3$ represents the cleanest point of inflection.
- **Silhouette Metrics:** The silhouette coefficients map structural separation across individual data points. The score drops off heavily past higher dimensions, confirming that a smaller subset of macro profiles ($K=3$) holds the tightest cohesion without over-segmenting.

---

## 2. Dimensionality Reduction & Cluster Interpretation
- **PCA Visualization:** Because multi-dimensional spacing cannot be read natively, Principal Component Analysis (PCA) was used to compress feature variances down into a two-dimensional scatter plot map (`cluster_visual_map.png`).
- **Profile Profiles ($K=3$):**
  - **Cluster 0 (Moderate-Activity Assets):** Characterized by steady average daily volumes and balanced baseline metric distributions.
  - **Cluster 1 (High-Volatility / High-Volume Spikes):** Represents high-momentum trading periods marked by wider shifts in indicators.
  - **Cluster 2 (Low-Momentum Segments):** Shows stagnant trading volume with near-static moving trends.

---

## 3. Mathematical Foundations
- **Inertia (Within-Cluster Sum of Squares):** $$\text{Inertia} = \sum_{i=1}^{n} \min_{\mu_j \in C} (||x_i - \mu_j||^2)$$
  - Tracks distance minimization from individual vectors to their local assigned cluster centroids.
- **Silhouette Coefficient:**
  $$s(i) = \frac{b(i) - a(i)}{\max(a(i), b(i))}$$
  - Where $a(i)$ represents inside-cluster intra-distance cohesion, and $b(i)$ maps nearest neighboring-cluster boundary separation.
