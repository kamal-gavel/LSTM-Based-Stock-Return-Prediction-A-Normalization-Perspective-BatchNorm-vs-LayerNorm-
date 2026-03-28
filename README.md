This repository presents a systematic study of normalization techniques in LSTM-based financial time series forecasting, with a focus on stock return prediction. Unlike conventional approaches that model raw prices, this work adopts a return-based framework to ensure stationarity and improve learning stability.

The core objective is to evaluate how different normalization strategies—No Normalization, Batch Normalization, and Layer Normalization—affect predictive performance and economic relevance.

🎯 Research Motivation

Financial time series are inherently:

Non-stationary
Noisy
Temporally dependent

Traditional deep learning pipelines often fail to account for these properties. In particular, Batch Normalization, while effective in computer vision, can disrupt temporal dependencies in sequential models.

This project investigates:

Does normalization improve LSTM performance in financial forecasting? If so, which method is most appropriate?

⚙️ Methodology
🔹 Data
Historical stock data from Yahoo Finance
Indian equities:
RELIANCE
HDFCBANK
INFOSYS
🔹 Feature Engineering

We transform raw prices into log returns:

𝑟
𝑡
=
log
⁡
(
𝑃
𝑡
𝑃
𝑡
−
1
)
r
t
	​

=log(
P
t−1
	​

P
t
	​

	​

)

This ensures:

Stationarity
Better convergence
Reduced trend bias

Additional technical indicators:

RSI (Relative Strength Index)
MACD (Moving Average Convergence Divergence)
Bollinger Bands
🔹 Model Architecture

We use a standard LSTM-based sequence model:

Input: Sliding window of past observations
Hidden layer: 64 LSTM units
Output: Future return prediction

Three normalization variants:

Model Variant	Description
NoNorm	Baseline LSTM
BatchNorm	Normalization across batch dimension
LayerNorm	Normalization across feature dimension
📊 Evaluation Metrics

We evaluate models using both statistical and financial metrics:

📉 Statistical
RMSE (Root Mean Squared Error)
R² (Coefficient of Determination)
📈 Financial
Directional Accuracy (DA)
→ Percentage of correctly predicted return direction
Trading PnL
→ Simple long/short strategy based on predictions
🔍 Key Findings
✅ 1. Returns outperform price modeling

Predicting returns leads to more stable learning and meaningful evaluation.

⚠️ 2. Batch Normalization is unsuitable for time series

BN introduces instability due to dependence on batch statistics, which breaks temporal structure.

🚀 3. Layer Normalization improves sequential learning

LN provides:

Better stability
Improved directional accuracy
More consistent trading performance
📊 4. Economic significance matters

Even when R² is low, models can still generate positive PnL, highlighting the importance of financial evaluation beyond traditional metrics.

🧪 Experimental Setup
Sequence Length: 60 timesteps
Prediction Horizons:
t+1 (short-term)
t+3 (medium-term)
t+5 (longer-term)
Optimizer: Adam
Loss Function: MSE
Gradient Clipping applied
🚀 How to Run
pip install -r requirements.txt
python src/train.py
