# My Capstone Project - Part 4 

This folder contains the Time Series sequential engineering layouts, Deep Learning LSTM configurations, and final loss performance validation graphs for Part 4 of the Capstone project.

---

## 1. Time Series Data Preparation & Splits
- **Timeline Constraints:** Financial price data is heavily reliant on chronological order. If specific date sequences were absent, a uniform daily dateline tracking column was generated to preserve data tracking.
- **Sequential Splitting:** Unlike static classification sets, a traditional random split **cannot** be used here. Shuffling data causes lookahead bias (data leakage). Instead, a pure chronological 80% train and 20% test partition boundary was implemented.
- **Window Engineering:** A sliding window frame with a **lookback value of 10 days** was constructed. The network evaluates the structural fluctuations of the previous 10 days to calculate its next price target value.

---

## 2. LSTM Deep Learning Architecture
- **Layer Configurations:** The model uses two stacked LSTM layers (50 memory cells each) to process sequential trend patterns effectively.
- **Regularization:** A `Dropout(0.2)` layer was added after each hidden node segment. This random node deactivation technique explicitly lowers variance to prevent overfitting.
- **Loss Optimization:** The framework implements an **Adam Optimizer** minimizing a **Mean Squared Error (MSE)** objective function over training epochs.

---

## 3. Evaluation Analysis
- **Price Forecast Interpretation:** The output values were converted back from their $(0, 1)$ scaled brackets into real monetary valuations using `.inverse_transform()`. 
- **Error Metrics:** The model's predictive accuracy was evaluated using Mean Squared Error (MSE) and Root Mean Squared Error (RMSE). The loss graphs confirm consistent convergence between the training and validation lines, showing the model learned clean patterns without memorizing the noise.
